скачала 3 рана по ссылкам:
https://www.ncbi.nlm.nih.gov/sra/SRX24513622[accn]
https://trace.ncbi.nlm.nih.gov/Traces/?view=run_browser&acc=SRR28984503&display=download
https://www.ncbi.nlm.nih.gov/sra/SRX24513633[accn]

разделить PairEnd на 2 SingleEnd

```
cat SRR28984503.fastq | grep '^@.*/1$' -A 3 --no-group-separator > SRR28984503_1.fastq
cat SRR28984503.fastq | grep '^@.*/2$' -A 3 --no-group-separator > SRR28984503_2.fastq
cat SRR28984716.fastq | grep '^@.*/1$' -A 3 --no-group-separator > SRR28984716_1.fastq
cat SRR28984716.fastq | grep '^@.*/2$' -A 3 --no-group-separator > SRR28984716_2.fastq
cat SRR28984726.fastq | grep '^@.*/1$' -A 3 --no-group-separator > SRR28984726_1.fastq
cat SRR28984726.fastq | grep '^@.*/2$' -A 3 --no-group-separator > SRR28984726_2.fastq
```
