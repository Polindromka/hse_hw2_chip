# hse_hw2_chip
- [x] Клеточная линия "Panc1"
- [x] Гистоновая метка "H3K4me3"
- [x] Реплика 1 "ENCFF000VIV"
- [x] Реплика 2 "ENCFF000VIX" 
- [x] Контроль "ENCFF000VJK" 
- [x] Хромосома 19 
## Ссылка на колаб:
```
https://colab.research.google.com/drive/12-qelkrRcmU7LBn52GyvvAMxoQs7JAqa?usp=sharing
```
## FASTQC
Было использовано выравнивание. Пример:
```python
!trimmomatic SE -phred33 /content/drive/MyDrive/bioinformatics/ENCFF000VIV.fastq ENCFF000VIV_trimmed.fastq ILLUMINACLIP:TruSeq3-SE:2:30:10 \
  LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36
```
- Однако, подрезание не улучшило значимо характиристики. 
- Замети, что именно контроль (ENCFF000VJK) показал наилучшие результаты (у остальных большое количество "ошибок"). 
- Заметим, что распределение GC content близко к нормальному для всех реплик. 
- Заметим, что per base sequence content дал хорошие показатели, только на контроле
- Заметим, что Per tile sequence quality дал хороший результат только на контроле

### ENCFF000VIV

**Basic Statistic**

Full | Trimmed
--- | --- 
![Image](images/ENCFF000VIV_basic_statistic.png) | ![Image](images/ENCFF000VIV_basic_statistic.png) 


**Per tile sequence quality**

Full | Trimmed
--- | --- 
![Image](images/ENCFF000VIV_per_tile.png) | ![Image](images/ENCFF000VIV_per_tile_trimmed.png) 

**Per base sequence content**

Full | Trimmed
--- | --- 
![Image](images/ENCFF000VIV_per_base_sequence.png) | ![Image](images/ENCFF000VIV_per_base_sequence_trimmed.png) 

**Per sequence GC content**

Full | Trimmed
--- | --- 
![Image](images/ENCFF000VIV_per_sequence_GC.png) | ![Image](images/ENCFF000VIV_per_sequence_GC_trimmed.png) 

### ENCFF000VIX

**Basic Statistic**

Full | Trimmed
--- | --- 
![Image](images/ENCFF000VIX_basic_statistic.png) | ![Image](images/ENCFF000VIX_basic_statistic.png) 


**Per tile sequence quality**

Full | Trimmed
--- | --- 
![Image](images/ENCFF000VIX_per_tile.png) | ![Image](images/ENCFF000VIX_per_tile_trimmed.png) 

**Per base sequence content**

Full | Trimmed
--- | --- 
![Image](images/ENCFF000VIX_per_base_sequence.png) | ![Image](images/ENCFF000VIX_per_base_sequence_trimmed.png) 

**Per sequence GC content**

Full | Trimmed
--- | --- 
![Image](images/ENCFF000VIX_per_sequence_GC.png) | ![Image](images/ENCFF000VIX_per_sequence_GC_trimmed.png) 

### ENCFF000VJK

**Basic Statistic**

Full | Trimmed
--- | --- 
![Image](images/ENCFF000VJK_basic_statistic.png) | ![Image](images/ENCFF000VJK_basic_statistic.png) 


**Per tile sequence quality**

Full | Trimmed
--- | --- 
![Image](images/ENCFF000VJK_per_tile.png) | ![Image](images/ENCFF000VJK_per_tile_trimmed.png) 

**Per base sequence content**

Full | Trimmed
--- | --- 
![Image](images/ENCFF000VJK_per_base_sequence.png) | ![Image](images/ENCFF000VJK_per_base_sequence_trimmed.png) 

**Per sequence GC content**

Full | Trimmed
--- | --- 
![Image](images/ENCFF000VJK_per_sequence_GC.png) | ![Image](images/ENCFF000VJK_per_sequence_GC_trimmed.png) 

## Выравнивание на 19 хромосому

Образец | Всего ридов | Выравнились 0 раз | Выравнились 1 раз | Выравнились > 1 раза | Общий процент выравнивания
--- | --- | --- | --- | --- | --- 
ENCFF000VIV | 32180108  | 28189186 | 2094036 | 1896886 | 12.40%
ENCFF000VIX | 21440042  | 18925664 | 1362134 | 1152244 | 11.73% 
ENCFF000VJK | 41671673  | 30686052 | 1659741 | 9325880 | 26.36%
## Venn
**ENCFF000VIV**

Venn 1 | Venn 2 
--- | --- 
![Image](images/venn1.png) | ![Image](images/venn2.png) 

**ENCFF000VIX**

Venn 1 | Venn 2 
--- | --- 
![Image](images/venn1_2.png) | ![Image](images/venn2_2.png) 


Заметим, что мы получили небольшой показатель пересечения. Его можно было бы улучшить с помощью параметров. Однако, эти показатели не сильно отличаются (пересечение MACS2 пиков и ENCODE и ENCODE и MACS2 пиков)

```python
!intervene venn -i /content/drive/MyDrive/bioinformatics/macs2/NA_peaks.broadPeak \
/content/drive/MyDrive/bioinformatics/ENCFF582SHP.bed --filenames --output \
/content/drive/MyDrive/bioinformatics/venn_results/venn1.jpg
```

```python
!intervene venn -i /content/drive/MyDrive/bioinformatics/ENCFF582SHP.bed \
/content/drive/MyDrive/bioinformatics/macs2/NA_peaks.broadPeak --filenames --output \
/content/drive/MyDrive/bioinformatics/venn_results/venn2.jpg
```

## NGS 
Так как в качестве образца использовалась гистоновая метка H3K4me3. То, судя по графикам, можем сказать, что наши результаты близки к результатам из статьи

Эксперимент | Статья
--- | --- 
![Image](images/ngs_plot.png) | ![Image](images/article.png) 
