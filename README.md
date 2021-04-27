# COVID-19_challenge

## About the Project
### Origin
The origin of this project stems from the COVID-19 Open Research Dataset challenge (CORD-19) launched by Kaggle in collaboration with the Allen Institute for AI and other organizations. The challenge can be found here: https://www.kaggle.com/allen-institute-for-ai/CORD-19-research-challenge/. The project was developed under the contex of the Text, Web and Social Media Analytics Lab course from the M.Sc. in Business Intelligence & process Management offered by the Berlin School of Economics and Law. 3 students worked together to achieve these results, during the course of the summer semester 2020.

### Objective
Within the original Kaggle challenge, there were many tasks aimed at exploring different aspects of the COVID-19 pandemic. For this project, the focus lied on:
* Effectiveness of case isolation/isolation of exposed individuals (i.e. quarantine)
* Effectiveness of community contact reduction (i.e. social distancing)

The aim was to summarize what literature posits on these two factors, by creating summary tables of the relevant papers. The official Kaggle submission was a summary table composed of 11 columns (i.e. Date, Study, Study Link, Journal, Study Type, Factors, Influential, Excerpt, Measure of Evidence, Added on DOI, CORD_UID). However, given the time limitations of this project, the team decided to focus on two of these columns, namely the Excerpt and Measure of Evidence.

Excerpt is here defined as a summary of the main findings of a paper. Measure of evidence, on the other hand, can be described as the conditions under which the study was carried out, more specifically timeline and location.

The research question here pursued is therefore: *“How can we mine for and summarize the findings on COVID-19 papers about quarantine and social distancing in the CORD-19 challenge dataset?”*

## Approach
### Paper filtering
Done with a user-defined function based on regular expressions extract only rhe relevant articles for the task. The group created three lists, each containing several synonyms for the COVID-19, quarantine, and social distancing, respectively. Then, the function checked whether any of the synonyms were present either in the title or the abstract of the paper. Only papers containing any synonym in either the title or abstract were selected.

### Conclusion Extraction
Done with a self-defined function, also based on regular expressions, that would parse the original data in json format and retrieve the paragraph only if the section title contained one of the predefined words (i.e. Conclusion, Summary, Outcomes, Discussion, etc.).

### LDA Topic Modelling
The filtering method described in the previous section selected papers that mentioned both quarantine or social distancing and the COVID-19. However, this did ensure that these papers evaluated the *effectiveness* of these measures in the spread of the pandemics. Thus, a more sophisticated model was needed as an additional step to single out only the papers relevant to the task (i.e. those addressing the effects of social distancing and quarantine on the COVID-19 spread). LDA Topic Modelling was chosen to fulfill this purpose. The team ran the model with 9 topics and chose those which had an interesting composition(e.g. 0.045*"model" + 0.033*"policy" + 0.019*"effect" + 0.019*"strategy" + 0.016*"social" + 0.014*"measure" + 0.014*"lockdown" + 0.013*"risk" + 0.013*"result" + 0.013*"differ").

### Summarization with BertSumExt
For deriving the excerpt column, the team chose to apply a text summarization technique. We used the BertSumExt model, available in this repo:https://github.com/hsiehkl/PreSumm


## Named Entity Recognition with spaCy
To retrieve the Measure of Evidence column for the Summay tables, which depicts the settings of the study (i.e. the locations and timeline), the team decided to use  Named Entity Recognition by spaCy’s NER model. Documentation of this package can be found here: https://spacy.io/usage/linguistic-features#named-entities

## Results
Two Summary tables: one containing 477 entried for Effectiveness of Quarantine conclusions and another of 537 records for Effectiveness of Social Distancing conclusions. Both of them had 3 columns> paper_id, Excerpt, and Measure of Evidence.

## Conclusion
The team effectively filtered for relevant scientific articles and used a unique methodology for extracting the columns for summary tables. The methodology that we used yielded the desired results, although there is still much room for improvement.
