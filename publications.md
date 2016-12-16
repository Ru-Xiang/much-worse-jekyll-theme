---
layout: page
permalink: /publications/
pubs:

    - title:   "SCOPE: Scalable Composite Optimization for Learning on Spark"
      author:  "Shen-Yi Zhao, Ru Xiang, Ying-Hao Shi, Peng Gao, Wu-Jun Li"
      journal: "Proceedings of the 31th AAAI Conference on Artificial Intelligence"
      note:    "AAAI"
      year:    "2017"
      url:     "http://arxiv.org/abs/1602.00133"
      pdf:     "https://arxiv.org/pdf/1602.00133v5.pdf"
          
    - title:   "Lock-Free Optimization for Non-Convex Problems"
      author:  "Shen-Yi Zhao, Gong-Duo Zhang, Wu-Jun Li"
      journal: "Proceedings of the 31th AAAI Conference on Artificial Intelligence"
      note:    "AAAI"
      year:    "2017"
      url:     "http://cs.nju.edu.cn/lwj/paper/AAAI17_LFnonConvex.pdf"
      pdf:     "http://cs.nju.edu.cn/lwj/paper/AAAI17_LFnonConvex.pdf"

    - title:   "Fast Asynchronous Parallel Stochastic Gradient Descent: A Lock-Free Approach with Convergence Guarantee"
      author:  "Shen-Yi Zhao, Wu-Jun Li"
      journal: "Proceedings of the 30th AAAI Conference on Artificial Intelligence"
      note:    "AAAI"
      year:    "2016"
      url:     "http://www.aaai.org/ocs/index.php/AAAI/AAAI16/paper/view/12442"
      pdf:     "http://cs.nju.edu.cn/lwj/paper/AAAI16_AsySVRG.pdf"


---

## Publications

{% assign thumbnail="left" %}

{% for pub in page.pubs %}
[**{{pub.title}}**]({% if pub.internal %}{{pub.url | prepend: site.baseurl}}{% else %}{{pub.url}}{% endif %})<br />
{{pub.author}}<br />
*{{pub.journal}}*
{% if pub.note %} *({{pub.note}})*
{% endif %} *{{pub.year}}* {% if pub.pdf %}[[pdf]({{pub.pdf}})]{% endif %} {% if pub.codes %}[[codes]({{pub.codes}})]{% endif %}

{% endfor %}
