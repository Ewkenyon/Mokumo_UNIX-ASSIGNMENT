UNIX Assignment
Data Inspection
Attributes of fangetal_genotypes
Here are my snippets of codes used for data inspection By inspecting this file I learned that:
$ head -n3 fang_et_al_genotypes.txt
The file is too long to inspect with cat, therefore I used head to have a look at the top of the file. I specified the number of lines by using -n3 argument. ```
$ tail -n3 fangetal_genotypes.txt
I repeated what I did for head with tail, to see the end of the file, specifying how many last lines to include.
$ wc fang_et_al_genotypes.txt
I ran this code to see get the following information about the data: 2783 words, 2744038 lines, 11051939 characters
$ ls -lh fang_et_al_genotypes.txt
I ran the code above to get the size of the file, which happens to be 11M (megabytes).
$ awk -F "\t" '{print NF; exit}' fang_et_al_genotypes.txt
I used the code above to find the number of columns in the dataset to be 986. I set the argument to -F, to specify that the dataset should be tab-delimited.
$ grep -v "^#" fang_et_al_genotypes.txt | awk -F "\t" '{print NF; exit}'
The above code is useful if the datasets contains "#".
Attributes of snp_position.txt
I ran the same codes that I used to inspect fang et al genotypes, to inspect snp positions. The comments for the genotypes also apply for snp positions, except where specific numbers such as the number of columns or size of the file apply.
$ head -n3 snp_position.txt
$ tail -n3 snp_position.txt
$ wc snp_position.txt
984 words 13198 lines 82763 characters
$ ls -lh snp_position.txt
81K (kilobytes)
$ awk -F "\t" '{print NF; exit}' snp_position.txt
15 columns
$ grep -v "^#" snp_position.txt | awk -F "\t" '{print NF; exit}'
15 columns
Data Processing
$ sort -k3,3 fang_et_al_genotypes.txt | cut -f3 | uniq -c| column -t > extracted_column3_fang_et_al_genotypes.txt
I ran this code to sort the third column, extracted it out, count the number of occurences next to unique lines, arrange the column in order.
Maize data
$ awk -F "\t" '$3 ~ /ZMMIL|ZMMLR|ZMMMR|Group/' fang_et_al_genotypes.txt | cut -f 1,4-986 > maize_genotypes.txt
This code uses awk to extract the rquired maize groups from the fang et al genotypes. $ awk -f transpose.awk maize_genotypes.txt > transposed_maize_genotypes.txt
This code transposes the maize genotypes.
$ head -n 1 transposed_maize_genotypes.txt && tail -n +2 transposed_maize_genotypes.txt | sort -k1,1 > sorted_transposed_maize_genotypes.txt This code sorts out the transposed maize genotypes without including the head.
Teosinte data
$ awk -F "\t" '$3 ~ /ZMPBA|ZMPIL|ZMPJA|Group/' fang_et_al_genotypes.txt | cut -f 1,4-986 > teosinte_genotypes.txt This code uses awk to extract the required teosinte groups from the fang et al genotypes. ``` $ awk -f transpose.awk teosintegenotypes.txt > transposedteosinte_genotypes.txt
``` This code transposes the teosinte genotypes.
$ head -n 1 transposed_teosinte_genotypes.txt && tail -n +2 transposed_teosinte_genotypes.txt | sort -k1,1 > sorted_transposed_teosinte_genotypes.txt This code sorts out the transposed teosinte genotypes without including the head.
Extracted snp positions
$ cut -f1,3,4 snp_position.txt |column -t > extracted_snp_position.txt I ran this code to extract the required first, third and fourth columns of the snp data. $ head -n1 extracted_snp_position.txt && tail -n2 extracted_snp_position.txt |sort -k1,1 > sorted_snp_position.txt This code sorts without the extracted snp positions without including the head.
Joining genotypes with snp positions
Maize
$ join --header -1 1 -2 1 -t $'\t' sorted_snp_position.txt sorted_transposed_maize_genotypes.txt > joined_maize_snp_genotypes.txt This code joins the transposed maize dataset with snp dataset.
Teosinte
$ join --header -1 1 -2 1 -t $'\t' sorted_snp_position.txt sorted_transposed_teosinte_genotypes.txt > joined_teosinte_snp_genotypes.txt This code joins the transposed teosinte dataset with snp dataset
Chromosomes Files
Maize files in increasing snp position values
The missing nucleotide are represented by '?'. There was no need to replace them.
chromosome 1
$ head -n1 joined_maize_snp_genotypes.txt && awk '$2 == 1' joined_maize_snp_genotypes.txt | sort -k 3n > Chr1_maize_genotypes.txt
chromosome 2
$ head -n1 joined_maize_snp_genotypes.txt && awk '$2 == 2' joined_maize_snp_genotypes.txt | sort -k 3n > Chr1_maize_genotypes.txt
chromosome 3
$ head -n1 joined_maize_snp_genotypes.txt && awk '$2 == 3' joined_maize_snp_genotypes.txt | sort -k 3n > Chr1_maize_genotypes.txt
chromosome 4
$ head -n1 joined_maize_snp_genotypes.txt && awk '$2 == 4' joined_maize_snp_genotypes.txt | sort -k 3n > Chr1_maize_genotypes.txt
chromosome 5
$ head -n1 joined_maize_snp_genotypes.txt && awk '$2 == 5' joined_maize_snp_genotypes.txt | sort -k 3n > Chr1_maize_genotypes.txt
chromosome 6
$ head -n1 joined_maize_snp_genotypes.txt && awk '$2 == 6' joined_maize_snp_genotypes.txt | sort -k 3n > Chr1_maize_genotypes.txt
chromosome 7
$ head -n1 joined_maize_snp_genotypes.txt && awk '$2 == 7' joined_maize_snp_genotypes.txt | sort -k 3n > Chr1_maize_genotypes.txt
chromosome 8
$ head -n1 joined_maize_snp_genotypes.txt && awk '$2 == 8' joined_maize_snp_genotypes.txt | sort -k 3n > Chr1_maize_genotypes.txt
chromosome 9
$ head -n1 joined_maize_snp_genotypes.txt && awk '$2 == 9' joined_maize_snp_genotypes.txt | sort -k 3n > Chr1_maize_genotypes.txt
chromosome 10
$ head -n1 joined_maize_snp_genotypes.txt && awk '$2 == 10' joined_maize_snp_genotypes.txt | sort -k 3n > Chr1_maize_genotypes.txt
Maize files in decreasing snp position values
'sed'is used to replace '?'with '-'. 'g'is added for this replacement to happen everywhere '?'is present.
chromosome 1
$ head -n1 joined_maize_snp_genotypes.txt && awk '$2 == 1' joined_maize_snp_genotypes.txt | sort -k 3nr | sed 's/?/-/g' > Chr1_dcr_maize.txt
chromosome 2
$ head -n1 joined_maize_snp_genotypes.txt && awk '$2 == 2' joined_maize_snp_genotypes.txt | sort -k 3nr | sed 's/?/-/g' > Chr2_dcr_maize.txt
chromosome 3
$ head -n1 joined_maize_snp_genotypes.txt && awk '$2 == 3' joined_maize_snp_genotypes.txt | sort -k 3nr | sed 's/?/-/g' > Chr3_dcr_maize.txt
chromosome 4
$ head -n1 joined_maize_snp_genotypes.txt && awk '$2 == 4' joined_maize_snp_genotypes.txt | sort -k 3nr | sed 's/?/-/g' > Chr4_dcr_maize.txt``
chromosome 5
$ head -n1 joined_maize_snp_genotypes.txt && awk '$2 == 5' joined_maize_snp_genotypes.txt | sort -k 3nr | sed 's/?/-/g' > Chr5_dcr_maize.txt
chromosome 6
$ head -n1 joined_maize_snp_genotypes.txt && awk '$2 == 6' joined_maize_snp_genotypes.txt | sort -k 3nr | sed 's/?/-/g' > Chr1_dcr_maize.txt
chromosome 7
$ head -n1 joined_maize_snp_genotypes.txt && awk '$2 == 7' joined_maize_snp_genotypes.txt | sort -k 3nr | sed 's/?/-/g' > Chr7_dcr_maize.txt
chromosome 8
$ head -n1 joined_maize_snp_genotypes.txt && awk '$2 == 8' joined_maize_snp_genotypes.txt | sort -k 3nr | sed 's/?/-/g' > Chr8_dcr_maize.txt
chromosome 9
$ head -n1 joined_maize_snp_genotypes.txt && awk '$2 == 9' joined_maize_snp_genotypes.txt | sort -k 3nr | sed 's/?/-/g' > Chr9_dcr_maize.txt
chromosome 10
$ head -n1 joined_maize_snp_genotypes.txt && awk '$2 == 10' joined_maize_snp_genotypes.txt | sort -k 3nr | sed 's/?/-/g' > Chr10_dcr_maize.txt
maize snps with unknown positions
$ head -n1 joined_maize_snp_genotypes.txt && awk '$3 ~ /unknown/' joined_maize_snp_genotypes.txt > maize_snp_unknown_position.txt
maize snps with multiple positions
$ head -n1 joined_maize_snp_genotypes.txt && awk '$3 ~ /multiple/' joined_maize_snp_genotypes.txt > maize_snp_multiple_position.txtm
Teosinte files in increasing snp position values
chromosome 1
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$2 == 1' joined_teosinte_snp_genotypes.txt | sort -k 3n > Chr1_teosinte_genotypes.txt
chromosome 2
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$2 == 2' joined_teosinte_snp_genotypes.txt | sort -k 3n > Chr2_teosinte_genotypes.txt
chromosome 3
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$2 == 3' joined_teosinte_snp_genotypes.txt | sort -k 3n > Chr3_teosinte_genotypes.txt
chromosome 4
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$2 == 4' joined_teosinte_snp_genotypes.txt | sort -k 3n > Chr4_teosinte_genotypes.txt
chromosome 5
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$2 == 5' joined_teosinte_snp_genotypes.txt | sort -k 3n > Chr5_teosinte_genotypes.txt
chromosome 6
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$2 == 6' joined_teosinte_snp_genotypes.txt | sort -k 3n > Chr6_teosinte_genotypes.txt
chromosome 7
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$2 == 7' joined_teosinte_snp_genotypes.txt | sort -k 3n > Chr7_teosinte_genotypes.txt
chromosome 8
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$2 == 8' joined_teosinte_snp_genotypes.txt | sort -k 3n > Chr8_teosinte_genotypes.txt
chromosome 9
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$2 == 9' joined_teosinte_snp_genotypes.txt | sort -k 3n > Chr9_teosinte_genotypes.txt
chromosome 10
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$2 == 10' joined_teosinte_snp_genotypes.txt | sort -k 3n > Chr10_teosinte_genotypes.txt
Teosinte files in decreasing snp position values
'sed'is used to replace '?'with '-'. 'g'is added for this replacement to happen everywhere '?'is present.
chromosome 1
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$2 == 1' joined_teosinte_snp_genotypes.txt | sort -k 3nr | sed 's/?/-/g' > Chr1_dcr_teosinte.txt
chromosome 2
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$2 == 2' joined_teosinte_snp_genotypes.txt | sort -k 3nr | sed 's/?/-/g' > Chr2_dcr_teosinte.txt
chromosome 3
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$2 == 3' joined_teosinte_snp_genotypes.txt | sort -k 3nr | sed 's/?/-/g' > Chr3_dcr_teosinte.txt
chromosome 4
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$2 == 4' joined_teosinte_snp_genotypes.txt | sort -k 3nr | sed 's/?/-/g' > Chr4_dcr_teosinte.txt
chromosome 5
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$2 == 5' joined_teosinte_snp_genotypes.txt | sort -k 3nr | sed 's/?/-/g' > Chr5_dcr_teosinte.txt
chromosome 6
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$2 == 6' joined_teosinte_snp_genotypes.txt | sort -k 3nr | sed 's/?/-/g' > Chr6_dcr_teosinte.txt
chromosome 7
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$2 == 7' joined_teosinte_snp_genotypes.txt | sort -k 3nr | sed 's/?/-/g' > Chr7_dcr_teosinte.txt
chromosome 8
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$2 == 8' joined_teosinte_snp_genotypes.txt | sort -k 3nr | sed 's/?/-/g' > Chr8_dcr_teosinte.txt
chromosome 9
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$2 == 9' joined_teosinte_snp_genotypes.txt | sort -k 3nr | sed 's/?/-/g' > Chr9_dcr_teosinte.txt
chromosome 10
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$2 == 10' joined_teosinte_snp_genotypes.txt | sort -k 3nr | sed 's/?/-/g' > Chr10_dcr_teosinte.txt
teosinte snps with unknown positions
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$3 ~ /unknown/' joined_teosinte_snp_genotypes.txt > teosinte_snp_unknown_position.txt
teosinte snps with multiple positions
$ head -n1 joined_teosinte_snp_genotypes.txt && awk '$3 ~ /multiple/' joined_teosinte_snp_genotypes.txt > teosinte_snp_multiple_position.txt
