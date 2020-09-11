# IMNA
###  1. Introduction
------------
</br>

> **`IMNA`** is a integrative multi-omics network-based approach to capture genetic-driven regulatory networks for human complex diseases. This method can combine functional data from multiple biological scales to understand molecular mechanisms of disease and identify potential key genes. This pipeline provide several scripts facilitating data access, integration and analysis.

</br>

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

</br>

###  3. Tutorial
------------
</br>  

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
inpmoduledir          Directory of all gene module (gene list)
oup                   Prefix of output file
</pre>

##### Output file(s):  
> ***oup.txt***: Gene set (module)  
> ***oup_info.txt***: Module information  

</br><b>3.2 Constract bipartite based on SNP-gene pairs</b>
```bash
Script:
		2-Constract_bipartite.py

Usage:
		python3 ${IMNA_tk}/script/2-Constract_bipartite.py <GS pair> <oup>

```

##### Details for parameters:
<pre>
GS pair               Gene-SNP pairs 
oup                   Prefix of output file
</pre>

##### Output file(s):
> ***oup_DG_snp.txt***: Raw SNP degree score  
> ***oup_DG_gene.txt***: Raw gene degree score  
> ***oup_DG_gene.nor.txt***: Normalized gene degree score  

</br><b>3.3 KDA - Key driver analysis </b>
```bash
Script:
		3-KDA_analysis.py

Usage:
		python3 ${IMNA_tk}/script/3-KDA_analysis.py <GS pair> <modulefile> <oup>

```

##### Details for parameters:
<pre>
GS pair               Gene-SNP pairs
modulefile            module file, conducted by 1-Export_module.py
oup                   Prefix of output file
</pre>

##### Output file(s):
> ***oup_KDA-module.txt***: Gene module set  
> ***oup_KDA-score.txt***: Gene enrichment score  

</br><b>3.4 SS - Signature score analysis </b>
```bash
Script:
		4-Combine_bip_SScore.py

Usage:
		python3 ${IMNA_tk}/script/4-Combine_bip_SScore.py <inter_score> <module> <oup>

```

##### Details for parameters:
<pre>
inter_score           Interaction score of database (PPI, GIANT)
module                Gene set module (step 1 output)
oup                   Prefix of output file
</pre>

##### Output file(s):
> ***oup_SScore.txt***: Combined gene signiture score  

</br><b>3.5 CS - Composite score analysis </b>
```bash
Script:
		5-Composite_score.py

Usage:
		python3 ${IMNA_tk}/script/5-Composite_score.py <PPI_SScore> <GIANT_SScore> <oup>

```

##### Details for parameters:
<pre>
PPI_SScore            Gene signiture score of PPI network (step 4 output)
GIANT_SScore          Gene signiture score of GIANT network (step 4 output)
oup                   Prefix of output file
</pre>

##### Output file(s):
> ***oup_Composite_score.txt***: Gene composite score (PPI and GIANT network)  

</br>  


###  4. Example
------------
</br>

* Calculate gene composition score of 6 gene set modlue accoding to gene interaction from PPI and GIANT netwrok

```sh
###Step1:  

		python3 ${IMNA_tk}/script/1-Export_module.py ${IMNA_tk}/data/geneset module

        ## "module.txt"
		gene	module	moduleset
		SLC15A1	101	1
		FLOT1	101	1
		MTMR9	101	1
		C14orf135	101	1
		CMTM6	101	1
		DAAM1	101	1
		HOXA10	101	1
		ZNF84	101	1
		GMPR	101	1

        ## "module_info.txt"
		module	name
		101	263-signatures-ori.txt
		102	100-signatures-ori.txt
		103	300-signatures-ori.txt
		104	39-signatures-ori.txt
		105	126-signature-ori.txt
		106	14-signatures-ori.txt
```
```
###Step2:  

		python3 ${IMNA_tk}/script/2-Constract_bipartite.py snp.gene.pairs bip

		## "snp.gene.pairs"
		ENTREZID	SNP
		5243	rs185481544
		11086	rs28465148
		11086	rs7669284
		11086	rs11934547
		11086	rs28436676
		11086	rs59826661
		11086	rs4469051
		11086	rs7669051
		11086	rs4459969

		## "bip_DG_snp.txt"
		DG	Node
		0.02097902097902098	rs62064394
		0.006993006993006993	rs117404018
		0.006993006993006993	rs117916627
		0.006993006993006993	rs139268110
		0.006993006993006993	rs112746008
		0.006993006993006993	rs34719019
		0.006993006993006993	rs117187923
		0.006993006993006993	rs114433718
		0.02097902097902098	rs12150223

		## "bip_DG_gene.txt"
		DG	Node
		0.00022660321776569228	580
		0.00022660321776569228	752
		0.00022660321776569228	148345
		0.00022660321776569228	246744
		0.00022660321776569228	1021
		0.00022660321776569228	1267
		0.1907999093587129	1394
		0.00045320643553138455	1545
		0.00022660321776569228	83468

		## "bip_DG_gene.nor.csv"
		DG	Node	Norm
		0.22003172445048721	284058	1.0
		0.1907999093587129	1394	0.8670103092783505
		0.1470654883299343	4137	0.6680412371134021
		0.10151824155903014	9884	0.4608247422680412
		0.10061182868796738	474170	0.4567010309278351
		0.09811919329254476	51326	0.44536082474226807
		0.05030591434398369	389170	0.22783505154639178
		0.04146838885112169	8631	0.18762886597938144
		0.024699750736460458	100506084	0.11134020618556702


###Step3:  

		python3 ${IMNA_tk}/script/3-KDA_analysis.py PPI.txt  module.txt  PPI-KDA
		python3 ${IMNA_tk}/script/3-KDA_analysis.py GIANT.txt  module.txt  GIANT-KDA

		## ""

		## ""

		## ""


###Step4:  

		python3 ${IMNA_tk}/script/

		## ""

		## ""

		## ""


###Step5:  

		python3 ${IMNA_tk}/script/

		## ""

		## ""

		## ""


```

</br>


###  5. License
------------
</br>  

> This software is distributed under the terms of GPL 2.0
</br>


###  6. Source
------------
</br>  

> [https://github.com/xjtugenetics/IMNA](https://github.com/xjtugenetics/IMNA)
</br>


###  7. Contact
------------
</br>  

#### Author
> **Yi-Xiao Chen**, **Shan-Shan Dong**, **Yan Guo**, **Tie-Lin Yang**  
> Key Laboratory of Biomedical Information & Genetics Center, School of Life Science and Technology, Xi'an Jiaotong University, Xi'an, Shaanxi Province, 710049, P. R. China  
> [:email:](yangtielin@mail.xjtu.edu.cn) yangtielin@mail.xjtu.edu.cn  
</br>


###  8. Maintainer
------------
</br>  

> **Yi-Xiao Chen**  
> You can contact [:email:](aaa@stu.xjtu.edu.cn) aaa@stu.xjtu.edu.cn
  when you have any questions, suggestions, comments, etc.
> Please describe in details, and attach your command line and log messages if possible.  
</br>


###  9. Requiremnets
------------
</br>  
	
- **Python** ( >= 3.2 )
	- numpy( >=1.10.4)
	- mpmath( >=0.19)
	- pandas( >=0.18.0)
	- scipy( >= 0.17.0)
	- rpy2( >= 2.9.0)
- **R** \( >= 3.3.2 \)
</br>


###################### No pain, no gain. #############################

