# Домашнее задание №1

```
$ ls /usr/share/data-minor-bioinf/assembly/* | xargs -tI{} ln -s {}
```
```
$ seqtk sample -s 14122001 oil_R1.fastq 5000000 > PE1.fq
$ seqtk sample -s 14122001 oil_R2.fastq 5000000 > PE2.fq
$ seqtk sample -s 14122001 oilMP_S4_L001_R1_001.fastq 1500000 > MP1.fq
$ seqtk sample -s 14122001 oilMP_S4_L001_R2_001.fastq 1500000 > MP2.fq
```
```
$ rm *.fastq
$ ls -1 | xargs -tI{} fastqc {}
$ mkdir fastqc_raw
$ ls *.html -1 | xargs -tI{} mv -v {} fastqc_raw
$ ls *.zip -1 | xargs -tI{} mv -v {} fastqc_raw
$ multiqc fastqc_raw -o multiqc_raw
```
![image](https://user-images.githubusercontent.com/75699392/139101705-d863a488-6f70-4ac8-87a3-dd6251e20dbe.png)
![image](https://user-images.githubusercontent.com/75699392/139101801-360bd909-e185-4d08-ad6f-0d574d0eabb2.png)
![image](https://user-images.githubusercontent.com/75699392/139101863-8816f63a-a0a2-4370-b9b4-f5396665cbf4.png)
![image](https://user-images.githubusercontent.com/75699392/139101916-acbf70f1-525d-4995-abc8-d4c9ed0e2bd5.png)
![image](https://user-images.githubusercontent.com/75699392/139102266-0e02035f-e325-4eca-acc6-4d937dc3a74d.png)
```
$ platanus_trim PE1.fq PE2.fq
$ platanus_internal_trim MP1.fq MP2.fq
$ rm *.fq
```
```
$ mkdir fastqc_trimmed
$ ls *trimmed -1 | xargs -tI{} fastqc {} -o fastqc_trimmed
$ multiqc fastqc_trimmed -o multiqc_trimmed
```
![image](https://user-images.githubusercontent.com/75699392/139102617-4270b8cc-8d8d-4c23-8310-9b33f2a4f235.png)
![image](https://user-images.githubusercontent.com/75699392/139102657-accff891-8b13-40e8-ba09-9adf50f90b7a.png)
![image](https://user-images.githubusercontent.com/75699392/139102708-c5178a96-6374-41cc-8369-828303cc16f5.png)
![image](https://user-images.githubusercontent.com/75699392/139102755-cca87fc6-919e-42ef-acf2-2e84de7a6717.png)
![image](https://user-images.githubusercontent.com/75699392/139102858-aa779c09-dfb4-4f7c-a2db-a635cd3f2362.png)
```
$ screen -S eamarusev
$ bash
$ platanus assemble -o Poil -f PE1.fq.trimmed PE2.fq.trimmed 2> assemble.log
$ time platanus scaffold -o Poil -t 1 -c Poil_contig.fa -IP1 *.trimmed -OP2 *.int_trimmed 2> scaffold.log
$ platanus gap_close -o Poil -t 1 -c Poil_scaffold.fa -IP1 *.trimmed -OP2 *.int_trimmed 2> gapclose.log
```
### Результаты
![image](https://user-images.githubusercontent.com/75699392/139103565-6cc11da3-e636-428e-9101-3642fa5f3b20.png)
см. в src




