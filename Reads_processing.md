#### Trim MP reads using Nextclip (v1.3.1)
```
nextclip -i g.morbida_mp_R1.fastq -j g.morbida_mp_R2.fastq -o g.morbida_mp_nxtclip -t 5 -e
```
#### Concatenate R1 and R2 reads for categories A, B, C
```
cat g.morbida_mp_nxtclip_A_R1.fastq g.morbida_mp_nxtclip_B_R1.fastq g.morbida_mp_nxtclip_C_R1.fastq > g.morbida_ABC_mp_nxtclp_R1.fastq
```
```
cat g.morbida_mp_nxtclip_A_R2.fastq g.morbida_mp_nxtclip_B_R2.fastq g.morbida_mp_nxtclip_C_R2.fastq > g.morbida_ABC_mp_nxtclp_R2.fastq
```
#### Error corrected PE reads using BLESS V:0.16 ####
```
bless -read1 g.morbida_pe_R1.fastq -read2 g.morbida_pe_R2.fastq \
-kmerlength 21 -verify -notrim -prefix g.morbida_bless_k21
```
#### Trim BLESS corrected PE reads using Trimmomatic V0.32 
```
java -jar /opt/Trimmomatic-0.32/trimmomatic-0.32.jar PE -threads 4 \
-baseout g.morbida_corrk21_trimphred2 \
g.morbida_bless_k21.1.corrected.fastq \
g.morbida_bless_k21.2.corrected.fastq \
ILLUMINACLIP:/opt/Trimmomatic-0.32/adapters/TruSeq3-PE-2.fa:2:30:10 \
LEADING:2 TRAILING:2 SLIDINGWINDOW:4:2 MINLEN:30
```