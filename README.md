# Tiny tool for Hi-TOM genotyping data orgnization

<img width="1409" height="987" alt="Git上传-1770002204600" src="https://github.com/user-attachments/assets/077a9e14-83ea-4f5a-8829-78b1a0cf3200" />

After you upload your data to Hi-TOM website, you are likely to get results like this:
<img width="198" height="200" alt="Git上传-1770002747009" src="https://github.com/user-attachments/assets/3b8e7d42-9983-49b6-be34-95eab0867a5f" />

Each of them contain sequence and genotype information.
<img width="247" height="206" alt="Git上传-1770002788107" src="https://github.com/user-attachments/assets/06e3e4fd-086c-409c-80d5-dc27ba8a769a" />


Put the `*Sequence.xls` file in a single folder. That's all preparation you need for these data.
<img width="180" height="193" alt="Git上传-1770003746786" src="https://github.com/user-attachments/assets/7daa850c-eb01-4895-ab9e-f3b366e0a76a" />


# Pipeline
Clone the code from github.
```sh
git clone https://github.com/CharlesV555/Hi-TOM-table-orgnization.git
```
Enter the main.R by R.
<img width="632" height="196" alt="Git上传-1770002701691" src="https://github.com/user-attachments/assets/50c3ac0a-149e-4201-b477-bddf09fb8c3d" />


>[!Note] R requirement
>R version 4.5.1 (2025-06-13 ucrt) -- "Great Square Root"
>tidyverse-2.0.0
> openxlsx-4.2.8

follow the instruction in it.
<img width="1002" height="473" alt="Git上传-1770003792356" src="https://github.com/user-attachments/assets/5e52b2a5-1700-4e1c-9145-b34aec25faa8" />

# Example
original data:
<img width="641" height="577" alt="Git上传-1770003529722" src="https://github.com/user-attachments/assets/c900dd20-d030-4536-9f74-dd1303452beb" />


result:
<img width="641" height="577" alt="Git上传-1770003558668" src="https://github.com/user-attachments/assets/8b5a06e2-2337-4aa5-ab77-11b6b7854f37" />


yeah you still need to do a little manupilation.

That's all for this tiny tool. Goog luck !

---

# Principle(in case of debugging)
2 logics: reorgnise the data frame & judge the genotype based on signal information.
### data frame
<img width="1117" height="457" alt="Git上传-1770003991584" src="https://github.com/user-attachments/assets/27f82ee5-bcf6-4437-a31e-f9fa7aafd9e0" />

Apated from Liu et al., _Science China Life Sciences_, 2019.
The information extraction is based on this layout. If bug rise in the future, it may due to the change of layout.

### genotype judgement
<img width="709" height="158" alt="Git上传-1770004240386" src="https://github.com/user-attachments/assets/cf02461a-4e3e-4a1a-9306-102dc799c12e" />

Given the situation in Zhai-lab, I label samples with signals more than 2 as error.

# Reference
Liu, Q., Wang, C., Jiao, X., Zhang, H., Song, L., Li, Y., Gao, C., & Wang, K. (2019). Hi-TOM: A platform for high-throughput tracking of mutations induced by CRISPR/Cas systems. _Science China Life Sciences_, _62_(1), 1～7. [https://doi.org/10.1007/s11427-018-9402-9](https://doi.org/10.1007/s11427-018-9402-9)
