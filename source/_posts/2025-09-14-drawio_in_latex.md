---
layout: post
title: 几近完美支持 LaTeX 引用的可视化绘图解决方案
subtitle: LaTeX 的水太深
author: RuntimeEroor
categories: 工具
tags: [LaTeX, inkscape, draw.io] 
date: 2025-09-14
---
# 1. inkscape=true
在 LaTeX 中使用 `\includesvg[inkscapeLaTeX=true]{...}` 时，Inkscape 会将 SVG 图中文字交给 LaTeX 排版，而不是直接转成图形，这样图中文字就能与正文统一，并且像 `\cite{}` 这样的命令也能被识别执行，因此可以在图里成功引用文献。


# 2. 替换 \cite 的引用
替换 draw.io 输出的 xml 中的引用。
```python
import xml.etree.ElementTree as ET
import re
import sys

def add_bibtex_citations_to_drawio(xml_content: str) -> str:
    """
    Parses a draw.io XML string, finds short paper titles, and appends BibTeX citations.

    Args:
        xml_content: A string containing the XML content of the draw.io file.

    Returns:
        A string with the modified XML content including BibTeX citations.
    """
    title_to_bib_key_map = {
        "DGD": "labe2024dgd",
        "FHGS": "duan2025fhgs",
        "GaussianVLM": "halacheva2025gaussianvlm",
        "Feature 3DGS": "zhou2023feature",
        "Langsplat": "qin2023langsplat",
        "4D LangSplat": "li2025langsplat",
        "LEGaussians": "shi2023language",
        "CLIP-GS": "liao2024clip",
        "FMGS": "zuo2024fmgs",
        "FastLGS": "ji2024fastlgs",
        "SA4D": "ji2024segment",
        "econSG": "zhang2025econsg",
        "SeqAffordSplat": "li2025seqaffordsplat",
        "MaskField": "gao2024fast",
        "PanopticRecon++": "yu2025leverage",
        "Unified-Lift": "zhu2025rethinking",
        "Segment Any 3D Gaussians": "cen2023segment",
        "OpenGaussian": "wu2024opengaussian",
        "InstanceGaussian": "li2024instancegaussian",
        "SADG": "li2024sadg",
        "Gaussian Grouping": "ye2023gaussian",
        "Segment then Splat": "lu2025segment",
        "LabelGS": "zhang2025labelgs",
        "Semantic Gaussians": "guo2024semantic",
        "LUDVIG": "marrie2024ludvig",
        "Occam's LGS": "cheng2024occam",
        "Dr.Splat": "junseong2025splat",
        "OpenGS-Fusion": "yang2025opengs",
        "SAGD": "hu2024sagd",
        "Lifting by Gaussians": "chacko2025lifting",
        "THGS": "dai2025training",
        "3DSceneEditor": "yan20243dsceneeditor",
        "NVSMask3D": "fang2025nvsmask3d",
        "RT-GS2": "jurca2024gs2",
        "Large Spatial Model": "fan2024large",
        "SemanticSplat": "li2025semanticsplat",
        "Uni3R": "sun2025uni3r"
    }

    try:
        root = ET.fromstring(xml_content)
    except ET.ParseError as e:
        return f"Error parsing XML: {e}"

    sorted_titles = sorted(title_to_bib_key_map.keys(), key=len, reverse=True)

    for cell in root.findall(".//*[@value]"):
        original_value = cell.get("value")
        modified_value = original_value

        for title in sorted_titles:
            bib_key = title_to_bib_key_map[title]
            escaped_title = re.escape(title)
            pattern = r"(?<!\w)(" + escaped_title + r")(?!\w)"
            replacement = r"\1 \\cite{" + bib_key + "}"
            modified_value = re.sub(pattern, replacement, modified_value)

        cell.set("value", modified_value)

    return ET.tostring(root, encoding="unicode")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("用法: python cite.py test.xml")
        sys.exit(1)
    input_path = sys.argv[1]

    with open(input_path, "r", encoding="utf-8") as f:
        xml_file_content = f.read()

    modified_xml_output = add_bibtex_citations_to_drawio(xml_file_content)

    with open(input_path, "w", encoding="utf-8") as f:
        f.write(modified_xml_output)
```


# 3. 修改替换后的 SVG 的 width 与 textLength
因为替换后的引用占用了过宽的 width，首先需要在 draw.io 导入替换后的 xml，重新导出新的 SVG。修改新 SVG 中的 width 和 viewport 为老的 SVG 的数值。

```python
import sys
import xml.etree.ElementTree as ET

def get_svg_width_and_viewbox(svg_path):
    tree = ET.parse(svg_path)
    root = tree.getroot()
    width = root.get("width")
    viewBox = root.get("viewBox")
    return width, viewBox

def set_svg_width_and_viewbox(svg_path, width, viewBox):
    tree = ET.parse(svg_path)
    root = tree.getroot()
    if width:
        root.set("width", width)
    if viewBox:
        root.set("viewBox", viewBox)
    tree.write(svg_path, encoding="UTF-8", xml_declaration=True)

if __name__ == "__main__":
    if len(sys.argv) != 3:
        print("用法: python replace_svg_width.py old.svg new.svg")
        sys.exit(1)
    old_svg, new_svg = sys.argv[1], sys.argv[2]
    width, viewBox = get_svg_width_and_viewbox(old_svg)
    set_svg_width_and_viewbox(new_svg, width, viewBox)
```


```python
import xml.etree.ElementTree as ET
import os
import sys

def modify_svg_text_elements(svg_filepath):
    """
    Modifies all <text> elements in an SVG file by setting textLength="0"
    and lengthAdjust="spacing" to control the reported width for layout.

    This is particularly useful when LaTeX's inkscapeLaTeX=true option is used,
    and original <text> content (e.g., with \cite{}) leads to an oversized
    bounding box calculation by Inkscape.

    Args:
        svg_filepath (str): The path to the SVG file.
    """
    if not os.path.exists(svg_filepath):
        print(f"错误: 文件未找到于 '{svg_filepath}'")
        return

    ET.register_namespace('', "http://www.w3.org/2000/svg")

    try:
        tree = ET.parse(svg_filepath)
        root = tree.getroot()
        svg_ns = "{http://www.w3.org/2000/svg}"

        modified_count = 0
        for text_element in root.iter(f"{svg_ns}text"):
            text_element.set('textLength', '0')
            text_element.set('lengthAdjust', 'spacing')
            modified_count += 1

        if modified_count == 0:
            print("SVG中未找到或未修改任何 <text> 元素。")
        else:
            print(f"成功修改了 {modified_count} 个 <text> 元素。")
        try:
            ET.indent(tree, space="  ", level=0)
        except AttributeError:
            print("警告: ET.indent 不可用 (需要 Python 3.9+)。输出可能未美化。")

        tree.write(svg_filepath, encoding='UTF-8', xml_declaration=True)
        print(f"SVG文件 '{svg_filepath}' 已成功更新。")

    except ET.ParseError as e:
        print(f"解析SVG文件时出错: {e}")
        print("请确保它是一个有效的XML/SVG文件。")
    except Exception as e:
        print(f"发生未知错误: {e}")

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("用法: python text.py <SVG文件路径>")
        sys.exit(1)
    input_filepath = sys.argv[1]
    modify_svg_text_elements(input_filepath)
```

# 4. 神奇的垂直居中
仔细看，会发现在 LaTeX 渲染后，有些文字没有垂直居中。而且还与 `width=\textwidth` 有关，拷打 AI 也没有什么结论。考虑到使用频率，可以使用 `\raisebox{-.5\height}{Hello}` 自行微调。
