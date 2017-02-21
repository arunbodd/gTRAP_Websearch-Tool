# gTRAP_Websearch-Tool
An informative and cumulative database for data related to protein synthesis involving (Gene, Transcription factors, Splicing, Post-translational Modifications, Proteins).

##SQL Queries:

##Create query:

##Gene table
Create table Gene (Gene_Id varchar(20) NOT NULL PRIMARY KEY, Gene_Symbol varchar(30), Chromosome_pos varchar(10), Gene_Name varchar(30), Family_Name varchar(50));


##Transcription table
Create table Transcription( Transciprion_Factor_ID varchar(20) NOT NULL PRIMARY KEY, TF_Name varchar(50), Gene_ID varchar(20) FOREIGN KEY REFERENCES Gene(Gene_ID), Chromosome varchar(10), Start_site varchar(20), End_site varchar(20));


##Splicing table
Create table Splicing(SID varchar(20) NOT NULL PRIMARY KEY,Gene_ID varchar(20) FOREIGN KEY REFERENCES Gene(Gene_ID),Type varchar(20), Position int, length_change varchar(20), Protein_ID varchar(20) FOREIGN KEY REFERENCES Protein(Protein_ID));


##Protein table
Create table protein(Protein_ID varchar(20) NOT NULL PRIMARY KEY, Protein_Name varchar(20), Protein_Sequence varchar(450));


##Modification table
Create table Modification(Protein_ID varchar(20) NOT NULL PRIMARY KEY, Position int, Modification_Name varchar(50), Protein_sequence varchar(450));

##Variation table
Create table variation(Protein_ID varchar(20) FOREIGN KEY REFERENCES Protein(Protein_ID),Position int, Original varchar(100), variant varchar(150), Sequence varchar(450));

##Selecting only transcription factors with Gene Id:
Select g.Gene_ID, g.Gene_Symbol, g.Gene_Name, tf.Tf_Name, tf.Start_site, tf.End_site  from Gene G Transcription TF where TF.GeneId=G.Geneid 

##Selecting only Splicing wid Gene Query:
Select g.Gene_Name, g.Gene_ID, g.Gene_Symbol  s.SID, s.Type from Gene G Splicing S where S.GeneId=G.GeneId

##Selecting only Modification & Variations with Gene Query:
Select g. gene_Symbol, g.Gene_ID, g.Gene_Name, s.sid, s.type, tf.Transcription_Factor_Name, tf.Transcription_ID, m.modification_name, m.position, p.protein_name, V. original, v. variant, v.position from Gene g, Transcription tf, splicing s, protein p where g.Gene_ID=t.Gene_ID and g.Gene_ID=s.Gene_ID and tf.gene_id=g.gene_id and s.protein_id=p.protein_id and m.Protein_id=p.protein_ID and V.proteinID=p.proteinID

##Selecting only Proteins with Gene Query:
Select g.gene_ID, g.Gene_Name, p.Protein_ID, p.Protein_Name, s.Sid from gene g, protein p, splicing s where g.gene_ID=s.gene_ID and s.protein_ID=p.protein_ID


##COUNT VALUE IN ALL TABLES:

select count (*) from Gene;

select count (*) from Transcription;

select count (*) from Splicing;

select count (*) from  Protein;

select count (*) from Modification;

select count (*) from variation;
