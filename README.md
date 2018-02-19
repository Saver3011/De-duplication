# De-duplication
library(stringi)
library(stringr)
df=read.csv('Deduplication Problem - Sample Dataset.csv')
#Taking only the first name and last name
df$ln=str_extract(pattern = '[A-z]+',string = df$ln)
df$fn=str_extract(pattern = '[A-z]+',string = df$fn)
#Record Linkage problem
library(RecordLinkage)

mat=compare.dedup(df,blockfld=c(2),strcmp = c(1,3,4),strcmpfun = jarowinkler)
mat_df=mat$pairs
mat_df=mat_df[mat_df$ln>=0.8&mat_df$fn>=0.8,]
other_ids=c(1:nrow(df))[!c(1:nrow(df)) %in% unique(c(mat_df$id1,mat_df$id2))]

ids=unique(mat_df$id1)
ids=ids[!ids %in% mat_df$id2]
uniq_ids=c(other_ids,ids)
uniq_ids=sort(uniq_ids)
