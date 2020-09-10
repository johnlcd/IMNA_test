# IMNA
###  1. Introduction
> **`IMNA`** is a integrative multi-omics network-based approach to capture genetic-driven regulatory networks for human complex diseases. This method can combine functional data from multiple biological scales to understand molecular mechanisms of disease and identify potential key genes. This pipeline provide several scripts facilitating data access, integration and analysis.


###  2. Download and Configure
------------
</br><b>2.1 Download</b>
<pre>
	git clone https://github.com/xjtugenetics/IMNA.git
</pre>

</br><b>2.2 Configure</b>
<pre>
	export IMNA_tk=/path/to/IMNA
</pre>


###  3. Tutorial
------------
- **Workflow**  

![IMNA workflow](https://github.com/xjtugenetics/IMNA/blob/master/workflow.png)

</br><b>3.1 Export gene set and module information </b>
```bash
Script:
		1-Export_module.py
		
Usage:
		python3 ${IMNA_tk}/script/1-Export_module.py <inpmoduledir> <oup>

```

##### Details for parameters:  
<pre>
inpmoduledir          Directory of all gene module
oup                   Prefix of output file
</pre>

##### Output file(s):  
> ***oup.txt***: Gene set (module)  
> ***oupinfo.txt***: Module information  

</br><b>3.2 Constract bipartite based on SNP-gene pairs</b>
```bash
Script:
		2-Constract_bipartite.py

Usage:
		python3 ${IMNA_tk}/script/2-Constract_bipartite.py <GS pair> <oup>

```
</br>

> Details for parameters:
<pre>
GS pair               Gene-SNP pairs 
oup                   Prefix of output file
</pre>

> Output file(s):
<pre>
*op_DG_gene.nor.csv*: Normalized gene degree score
</pre>

</br><b>3.3 KDA analysis </b>
```bash
Script:
		3-KDA_analysis.py

Usage:
		python3 ${IMNA_tk}/script/3-KDA_analysis.py <GS pair> <modulefile> <oup>

```
</br>

> Details for parameters:
<pre>
GS pair               Gene-SNP pairs
modulefile            module file, conducted by 1-Export_module.py
oup                   Prefix of output file
</pre>

> Output file(s):
<pre>
*oup_KDA-module.txt*: 
*oup_KDA-score.txt*: 
</pre>

</br><b>3.4 </b>
```bash
Script:
		4-Combine_bip_SScore.py

Usage:
		python3 ${IMNA_tk}/script/

```
</br>

> Details for parameters:
<pre>


</pre>

> Output file(s):
<pre>

</pre>

</br><b>3.5 </b>
```bash
Script:
		5-Composite_score.py

Usage:
		python3 ${IMNA_tk}/script/

```
</br>

> Details for parameters:
<pre>


</pre>

> Output file(s):
<pre>

</pre>


</br><b>3.3 Output files</b>
<pre>
out.site.gz: Remained SNPs after filtering [chr site]
out.blocks.gz: Block file [chr start end block_length SNP_number SNPs]
out.TriangleV.gz: Region Pairwise R^2/D'
out.svg: Output plot in SVG format
out.png: Output plot in png format
out.pdf: Output plot in pdf format
</pre>


###  4. Example
------------

</br>See more detailed usage in the&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <b>[Chinese Documentation](https://github.com/BGI-shenzhen/LDBlockShow/blob/master/LDBlockShow_Manual_Chinese.pdf)</b>
</br>See more detailed usage in the&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <b>[English Documentation](https://github.com/BGI-shenzhen/LDBlockShow/blob/master/LDBlockShow_Manual_English.pdf)</b>
</br>See the example directory and  Manual.pdf for more detail.


* Example 1)  show Figure with Defaut LD Blocks

<pre>
#../../bin/LDBlockShow   -InVCF Test.vcf.gz   -OutPut  out   -Region  chr11:24100000:24200000  -OutPng -SeleVar 1
../../bin/LDBlockShow   -InVCF Test.vcf.gz   -OutPut  out   -Region  chr11:24100000:24200000  -OutPng -SeleVar 2
# [-SeleVar 1] is D',[-SeleVar 2] is RR ,[-SeleVar 3] are RR and D',[-SeleVar 4] are D' and RR # the default is D'
</pre>

![out.png](https://github.com/BGI-shenzhen/LDBlockShow/blob/master/example/Example1/out.png)


###  5. License
------------
> This software is distributed under the terms of GPL 2.0
</br>


###  6. Source
------------
> [https://github.com/xjtugenetics/IMNA](https://github.com/xjtugenetics/IMNA)
</br>


###  7. Contact
------------
#### Author
> **Yi-Xiao Chen**, **Shan-Shan Dong**, **Yan Guo**, **Tie-Lin Yang**  
> Key Laboratory of Biomedical Information & Genetics Center, School of Life Science and Technology, Xi'an Jiaotong University, Xi'an, Shaanxi Province, 710049, P. R. China  
> [:email:](yangtielin@mail.xjtu.edu.cn) yangtielin@mail.xjtu.edu.cn  
</br>


###  8. Maintainer
> **Yi-Xiao Chen**  
> You can contact [:email:](aaa@stu.xjtu.edu.cn) aaa@stu.xjtu.edu.cn
  when you have any questions, suggestions, comments, etc.
> Please describe in details, and attach your command line and log messages if possible.  
</br>


###  9. Requiremnets
------------
- Python ( >= 3.2 )
- **Python** \( recommended: python2.7 \)
	- numpy( >=1.10.4)
	- mpmath( >=0.19)
	- pandas( >=0.18.0)
	- scipy( >= 0.17.0)
	- rpy2( >= 2.9.0)
- **R** \( >= 3.3.2 \)
</br>


###################### No pain, no gain. #############################

