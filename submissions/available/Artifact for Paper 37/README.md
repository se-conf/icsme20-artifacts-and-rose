This archive contains the supplementary material for the paper "What Developers (Care to) Recall: An Interview Survey on Smaller Systems" by Jacob Krüger and Regina Hebig, accepted at ICSME 2020.

The folder "InterviewData" comprises all anonymized data connected to our interviews:

- SurveyTemplate.pdf is the semi-structured interview guide (Table 2, Section 3.2)
- IntervieweeeMeta is a csv file describing our interviewees in anonymized form (Section 3.3)
- OS1-4 comprises the interviewees' self-assessments (Section 4.3)
- IK1, IK2 IK3, IK4_5 comprise the answers to the last section of our survey (Sections 4.1 and 4.3)
- Correctness, Correctness_Code, and Correctness_Model comprise our ratings of the interviewees' answers (Sections 3.5, 4.2, and 4.3)
- TimesScienceFileEdits contains the time differences between file edits and the interview (Figure 3, Section 4.2)


The folder "LiteratureData" comprises all data connected to our literature review (Section 2.2):

- Collection_raw is a full collection of all data, and lists all publications
- ThemesFromClassifications comprises the final classification scheme based on the original authors' classifications
- Reclassification comprises the assignments of each question to specific themes and sub-themes based on our re-classification
- Ratings provides the ratings we normalized from the identified literature

The folder "R" comprises our R script and the corresponding csv files we used for plotting our figures and conducting statistical tests:

- script.R is the complete script with comments
- The remaining csv files are read by the script and comprise the "InterviewData" in a formatting the script can process