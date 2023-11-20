# Laboratory_journal
description of the work on metagenomics
Ход работы ДЗ_5
Я взяла необработанными данными 23andMе,“FixMyProfessor.com”
Цель работы:
1. Установить материнскую (мтДНК)гаплогруппу
2. Установить отцовскую гаплогруппу
3. Прокомментиновать полученные SNP
4. Извлечь клинически значимые SNP
5. Определить фенотипические признаки по необработанным данным (цвет волос, глаз, кожи)
6. Найти клинически значемые SNP у анализируемого мужчины.

Используя программу plink (которую широко используют в популяционной генетике). С помощью команды
plink —23file SNP_raw_v4_Full_20170514175358.txt --recode vcf --out snps_clean --output-chr MT --snps-only just-acgt
я получила файл  snps_clean.vcf . Этот файл содержит все проанализированные SNP.

 Для определения этнической принадлежности данного субъекта с использованием материнской (мтДНК) и отцовской (Y-хромосомы). Для материнской линии (мтДНК):
   - James Lick's mtHap utility: https://dna.jameslick.com/mthap/
   - HaploGrep 2: https://haplogrep.uibk.ac.at/
Определила, что материнская ДНК относится к H2a2a1 гаплогруппе
2. Для отцовской линии (Y-хромосома):
   - YSEQ mt Clade Finder: https://www.yseq.net/mtcladefinder.php
   - Ybrowse: https://ybrowse.org/human/
Отцовская ДНК относится к R1a гаплогруппе

Для определения цвета глаз, волос и кожи я использовала статью и сайт :
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3694299/
www.perplexity
Были обнаружены
rs12913832 A/G
rs16891982 C/G
В результате анализа данных SNP я сделала вывод, что у мужчины цвет глаз – карие. Цвет кожи – светло бежевый. Цвет волос - шатен. Аннотацию всех SNP, выбор клинически значимых я провела с помощью SnpEff/SnpSift.
Аннотацию всех SNP, выбор клинически значимых я провела с помощью SnpEff/SnpSift.
Командой:
java -jar ~(base) kjlkhl@Valentina:~/lab/Laboratory_journal/step_5/snpEff/SnpSift.jar annotate clinvar.vcf  snps_clean.>Затем я выполнила grep для поля с потенциальным диагнозом, командой:
snps_clean_snpsift_clinvar.vcf | grep CLNDN
Получила огромный файл который я отсортировала с помощью команды:
rg -om42 "CLNDN=[^;]*" snps_clean_snpsift_clinvar.vcf|sort|uniq -c|sort -rnk1|sed 's/not_specified//g;s/not_provided//g>
и получила набор из 23 заболеваний к которым анализируемый человек предрасположен.
(base) kjlkhl@Valentina:~/lab/Laboratory_journal/step_5$ rg -om42 "CLNDN=[^;]*" snps_clean_snpsift_clinvar.vcf|sort|uniq -c|sort -rnk1|sed 's/not_specified//g;s/not_provided//g'
23 CLNDN=
      1 CLNDN=||Macrocephaly-intellectual_disability-neurodevelopmental_disorder-small_thorax_syndrome
      1 CLNDN=||Cataract_6_multiple_types
      1 CLNDN=|Autosomal_recessive_early-onset_Parkinson_disease_6|
      1 CLNDN=||Atrial_fibrillation,_familial,_6
      1 CLNDN=|Radio-Tartaglia_syndrome
      1 CLNDN=|Parenti-mignot_neurodevelopmental_syndrome
      1 CLNDN=|Macrocephaly-intellectual_disability-neurodevelopmental_disorder-small_thorax_syndrome|
      1 CLNDN=|Immunodeficiency_14b,_autosomal_recessive|Combined_immunodeficiency_with_faciooculoskeletal_anomalies|Immunodeficiency_14
      1 CLNDN=Schwartz-Jampel_syndrome|Lethal_Kniest-like_syndrome|Connective_tissue_disorder|
      1 CLNDN=Obesity,_association_with
      1 CLNDN=Left_ventricular_noncompaction_8|
      1 CLNDN=Joubert_syndrome_25|
      1 CLNDN=Hypophosphatasia|
      1 CLNDN=Homocystinuria_due_to_methylene_tetrahydrofolate_reductase_deficiency|
      1 CLNDN=Homocystinuria_due_to_methylene_tetrahydrofolate_reductase_deficiency
      1 CLNDN=Familial_thoracic_aortic_aneurysm_and_aortic_dissection|Ehlers-Danlos_syndrome,_kyphoscoliotic_type_1|
      1 CLNDN=Dystonia,_childhood-onset,_with_optic_atrophy_and_basal_ganglia_abnormalities|
      1 CLNDN=Deficiency_of_hydroxymethylglutaryl-CoA_lyase
      1 CLNDN=Autosomal_recessive_spastic_paraplegia_type_78|Kufor-Rakeb_syndrome|Inborn_genetic_diseases. 




