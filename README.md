# Tiny tool for Hi-TOM genotyping data orgnization

### Introduction
Though Hi-TOM do offer analysis on genotype based on sequence information, it provide little information we need. This project is a tiny tool to extract genotype, specific mutation, and organise these data.

It determines the genotype with a `min_threshold` and a `compare_index`.
Signal <= `min_threshold` is abandent, and the sample without signal left won't be shown;
samples with more than 2 signals after filtering are marked as "error";
samples with only one signal are marked as correspondent type;
samples with 2 signals would compute the ratio of 2 figures, that within `compare_index` are marked as heterozygote, the rest marked as heterozygote with a "?".

```mermaid
graph TD
    A[Genotype Determination Start] --> B[Filter Signals by min_threshold]
    
    B --> C{Any signals > min_threshold?}
    C -->|No| D[No Output<br/>Sample Skipped]
    C -->|Yes| E[Normalize Remaining Signals]
    
    E --> F[Count Normalized Signals]
    
    F -->|Signals > 2| G[Mark as: Error<br/>Too Many Signals]
    F -->|Signals = 2| H[Calculate Ratio of Two Signals]
    F -->|Signals = 1| I[Mark as: Homozygous]
    
    H --> J{Ratio within<br/>compare_index range?}
    J -->|Yes| K[Mark as: Heterozygous]
    J -->|No| L[Mark as: Homozygous with ?<br/>Needs Review]
    
    G --> M[Output Result]
    I --> M
    K --> M
    L --> M
    
    style A fill:#e1f5fe
    style B fill:#fff3e0
    style C fill:#ffccbc
    style D fill:#f5f5f5
    style E fill:#fff3e0
    style G fill:#ffebee
    style I fill:#e8f5e8
    style K fill:#e8f5e8
    style L fill:#fff3e0
    style M fill:#f3e5f5
```

### To start with
\n
<img width="1409" height="987" alt="Git上传-1770002204600" src="https://github.com/user-attachments/assets/077a9e14-83ea-4f5a-8829-78b1a0cf3200" />

After you upload your data to Hi-TOM website, you are likely to get results like this:\n
<img width="198" height="200" alt="Git上传-1770002747009" src="https://github.com/user-attachments/assets/3b8e7d42-9983-49b6-be34-95eab0867a5f" />

Each of them contain sequence and genotype information.\n
<img width="247" height="206" alt="Git上传-1770002788107" src="https://github.com/user-attachments/assets/06e3e4fd-086c-409c-80d5-dc27ba8a769a" />


Put the `*Sequence.xls` file in a single folder. That's all preparation you need for these data.\n
<img width="180" height="193" alt="Git上传-1770003746786" src="https://github.com/user-attachments/assets/7daa850c-eb01-4895-ab9e-f3b366e0a76a" />


# Pipeline

File structure:
```sh
C:.
│  .gitignore
│  filetree.txt
│  LICENSE
│  README.md # instruction
│  
└─genotyping_result_analysis
        .Rhistory
        genotyping_result_analysis.R # core function, single version
        genotyping_result_analysis.Rproj
        genptype_marking_func.R # core function, function version
        main.R # you only need to run this
        summarize_data_in_folder_func.R # read data

```

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

### 注意ATTENTION
<img width="268" height="161" alt="Tiny tool for Hi-TOM genotyping data orgnization-1770018191459" src="https://github.com/user-attachments/assets/edc6f27d-ff8e-46fc-bde7-1649ac67d365" />

文件名中的***CAF1X***非常重要，示例中不同CAF基因数据能够分列展示就是依靠对文件名的正则识别进行的。如果你需要测试自己的基因命名，最后表格中名字分类只会有一类“CAF1_unknown”。可以修改`genotype_marking`相关的代码实现你的分类。
It deserves your attention that the ***CAF1X*** part in names of original file is *SUPER IMPORTANT*. The division of columes in example is based on recognition of such part in file name using orthognal expressions. If you test your own data with different names, all these data would be displayed in only one colume named "CAF1_unknown". You may modify the part in `genotype_marking` to achieve proper sorting.
<img width="598" height="200" alt="Tiny tool for Hi-TOM genotyping data orgnization-1770017828172" src="https://github.com/user-attachments/assets/bb8c4d00-f34b-4e34-88f5-8777aa3b9962" />


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
