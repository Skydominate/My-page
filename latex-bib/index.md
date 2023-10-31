# Latex 导言区


***论文写作参考文献格式设置介绍***

<!--more-->

## Bibtex 的条目类型简介及引用

- 期刊论文：**article**: any article published in a periodical like a journal or magazine article

```markdown
@article{CitekeyArticle,
  author   = "P. J. Cohen",
  title    = "The independence of the continuum hypothesis",
  journal  = "Proceedings of the National Academy of Sciences",
  year     = 1963,
  volume   = "50",
  number   = "6",
  pages    = "1143--1148",
}
```

- 书籍：**book**: a book

```markdown
@book{CitekeyBook,
  author    = "Leonard Susskind and George Hrabovsky",
  title     = "Classical mechanics: the theoretical minimum",
  publisher = "Penguin Random House",
  address   = "New York, NY",
  year      = 2014
}
```

- 小册子：**booklet**: like a book but without a designated publisher

```markdown
@booklet{CitekeyBooklet,
  title        = "Canoe tours in {S}weden",
  author       = "Maria Swetla", 
  howpublished = "Distributed at the Stockholm Tourist Office",
  month        = jul,
  year         = 2015
}
```

- 会议论文：**conference**: a conference paper

- 书籍中的一个章节：**inbook**: a section or chapter in a book

```markdown
@inbook{CitekeyInbook,
  author    = "Lisa A. Urry and Michael L. Cain and Steven A. Wasserman and Peter V. Minorsky and Jane B. Reece",
  title     = "Photosynthesis",
  booktitle = "Campbell Biology",
  year      = "2016",
  publisher = "Pearson",
  address   = "New York, NY",
  pages     = "187--221"
}
```

- 文集中的一篇文章：**incollection**: an article in a collection

```markdown
@incollection{CitekeyIncollection,
  author    = "Shapiro, Howard M.",
  editor    = "Hawley, Teresa S. and Hawley, Robert G.",
  title     = "Flow Cytometry: The Glass Is Half Full",
  booktitle = "Flow Cytometry Protocols",
  year      = 2018,
  publisher = "Springer",
  address   = "New York, NY",
  pages     = "1--10"
}
```

- 会议论文：**inproceedings**: a conference paper (same as the conference entry type)

```markdown
@inproceedings{CitekeyInproceedings,
  author    = "Holleis, Paul and Wagner, Matthias and Koolwaaij, Johan",
  title     = "Studying mobile context-aware social services in the wild",
  booktitle = "Proc. of the 6th Nordic Conf. on Human-Computer Interaction",
  series    = "NordiCHI",
  year      = 2010,
  pages     = "207--216",
  publisher = "ACM",
  address   = "New York, NY"
}
```

- 技术手册：**manual**: a technical manual

```markdown
@manual{CitekeyManual,
  title        = "{R}: A Language and Environment for Statistical Computing",
  author       = "{R Core Team}",
  organization = "R Foundation for Statistical Computing",
  address      = "Vienna, Austria",
  year         = 2018
}
```

- 硕士论文：**masterthesis**: a Master's thesis

```markdown
@mastersthesis{CitekeyMastersthesis,
  author  = "Jian Tang",
  title   = "Spin structure of the nucleon in the asymptotic limit",
  school  = "Massachusetts Institute of Technology",
  year    = 1996,
  address = "Cambridge, MA",
  month   = sep
}
```

- 如果没有其他合适的：**misc**: used if nothing else fits

```markdown
@misc{CitekeyMisc,
  title        = "Pluto: The 'Other' Red Planet",
  author       = "{NASA}",
  howpublished = "\url{https://www.nasa.gov/nh/pluto-the-other-red-planet}",
  year         = 2015,
  note         = "Accessed: 2018-12-06"
}
```

- 博士论文：**phdthesis**: a PHD thesis

```markdown
@phdthesis{CitekeyPhdthesis,
  author  = "Rempel, Robert Charles",
  title   = "Relaxation Effects for Coupled Nuclear Spins",
  school  = "Stanford University",
  address = "Stanford, CA",
  year    = 1956,
  month   = jun
}
```

- 整个会议：**proceedings**: the whole conference proceedings

```markdown
@proceedings{CitekeyProceedings,
  editor    = "Susan Stepney and Sergey Verlan",
  title     = "Proceedings of the 17th International Conference on Computation and Natural Computation, Fontainebleau, France",
  series    = "Lecture Notes in Computer Science",
  volume    = "10867",
  publisher = "Springer",
  address   = "Cham, Switzerland",
  year      = 2018
}
```

- 科技报告：**techreport**: a technical report, government report or white paper

```markdown
@techreport{CitekeyTechreport,
  title       = "{W}asatch {S}olar {P}roject Final Report",
  author      = "Bennett, Vicki and Bowman, Kate and Wright, Sarah",
  institution = "Salt Lake City Corporation",
  address     = "Salt Lake City, UT",
  number      = "DOE-SLC-6903-1",
  year        = 2018,
  month       = sep
}
```

- 未正式发表的作品：**unpublished**: a work that has not yet been officially published

```markdown
@unpublished{CitekeyUnpublished,
  author = "Mohinder Suresh",
  title  = "Evolution: a revised theory",
  year   = 2006
}
```

___

*参考资料*
[A complete guide to the BibTeX format](https://www.bibtex.com/g/bibtex-format/#:~:text=Here%20is%20a%20complete%20listing%20of%20the%20BibTeX,paper%20%28same%20as%20the%20conference%20entry%20type%29%20%E6%9B%B4%E5%A4%9A%E9%A1%B9%E7%9B%AE)
[The 14 BibTeX entry types](https://www.bibtex.com/e/entry-types/)
