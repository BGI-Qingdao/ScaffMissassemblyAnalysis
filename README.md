# INSTALL

## step 1 , download all source codes.

>  git clone --recursive  https://gitlab.com/BGIQD/ScaffMissassemblyAnalysis.git

or 

> git clone https://gitlab.com/BGIQD/ScaffMissassemblyAnalysis.git

> cd ScaffMissassemblyAnalysis/

> git submodule init

> git submodule update

## step 2 , compile source code

>  cd codes && make && cd -

# USAGE 

## create a clean folder for your project

> mkdir test && cd test 

## run pipeline with correct arguments 

> installed_path/ScaffNGAReason.sh quast_contig.tsv quast_scaffold.tsv xxx.scaff_infos min_n min_c

## example 

> xxx/ScaffNGAReason.sh  chr21_quast/contigs_reports/all_alignments_chr21.tsv \\\
>  chr21_ogc1/contigs_reports/all_alignments_chr21_noverlap_new-scaff_seqs.tsv \\\
>  test/chr21_noverlap_new.scaff_infos 11 11

## output example 

     26 GapError10K
      4 GapError1K
      1 OrderError
     21 OrderUnknow
     23 OrientationError

# BRIEF 

       this script used to classify each missassmbly of quast_NGA of scaffold.
       current support types are :
           +--contig missassmbly
           |
           +--scaffold missassbbly
             +
             |
             +-- Order Unknow (contig repeat/contig unaligned/translocate...)
             |
             +-- Order Error  ( scaffold rank 1 but not ref rank 1/-1 )
             |
             +-- Orientation Error (Order correct but orientation diff in ref)
             |
             +-- Gap 1K (Order & orientation correct , n < 10 , gap_diff>1K)
             |
             +-- Gap 10K (Order & orientation correct , n >=10 ,gap_diff>10K)

       each missambly will belong to one of those types .
