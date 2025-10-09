### White Blood Cell (WBC) image recognition


In Medical laboratory medicine WBCs are used to diagnose medical conditions. A blood smear is prepared on a glass slide and then analyzed under a microscope. The laboratory professional then counts at least 100 WBCs to create a percentage that is multiplied by the total number of WBCs per volume of blood. This creates WBC absolute counts that are sent to the doctor to create a diagnosis. This process is called a manual (WBC) differential.
In this project we will be looking at six types of WBCs:


•	Immature Granules- These are precursors to mature white blood cells, and their presence indicates infection or cancer.


•	Basophil- These are associated with allergies.


•	Eosinophils- These are associated with allergies.


•	Lymphocytes- These create a specific immune response by creating antibodies. They are also known as B cells, T cells, and Plasma cells. 


•	Neutrophils- These respond to general bacterial infections and nonspecific immune reactions.


•	Monocytes- These WBCs phagocytize pathogens. They are also known as mast cells when found in tissues.


Automating manual differentials using image recognition can enable short staffed medical laboratories to have more time to perform other patient testing. There are not enough certified professionals in the USA to fully staff medical laboratories. Due to an aging workforce retiring and the ageing USA baby boomer population, staffing shortages will likely continue to increase across the country. Having the option of buying a more automated laboratory allows hospitals to keep existing staffing levels while increasing laboratory testing through put. It also helps to keep lab turnaround times low for emergency situations. 


### Data


A data set of blood cell images was taken from Kaggle. The data set has 17,092 images taken from a CellaVision DM96 analyzer. The images include neutrophils, eosinophils, basophils, lymphocytes, monocytes, immature granulocytes, erythroblasts, and platelets. All original images are 224 x 224 pixels in color.


### Data Cleaning


The erythroblasts and platelets were not used in this analysis. All other cell images were individually checked to make sure they were sorted into the correct cell category by a professional hematologist.


### EDA


All images were confirmed as RBG images and resized to 100 x 100 pixels. The images were then made into arrays, flattened, and scaled by dividing by 255. These arrays were saved in a pandas data frame labeled with their respective cell type.


### Modeling


A K nearest neighbor model was created. Optimal KNN was found to be 13. The model evaluation can be seen in the metrics file under Notebooks.


KNN performed poorly with an overall accuracy of 0.54 and bad ROC AUC scores.


A random forest model was created using the data set. The model evaluation can be seen in the metrics file under Notebooks.


The random forest model performs significantly better than the KNN with an accuracy of 0.79


A CNN model was created using the data frame. The model evaluation can be seen in the metrics file under Notebooks.
	

The CNN model worked significantly better than the other models. It had an accuracy score of 0.92 and all the ROC AUC scores were above 0.95. It only misclassified If cells which is common in analyzers. This error is what causes a manual differential to be ordered for lab testing.


The CNN model was chosen as the best model for this project based on its statistics. Also, image processing works better with neuronets. 


### Discussion


The final model created from this analysis performs very well. It has high AUC scores across the six chosen cell types, and an overall accuracy around 0.92.  Looking at the confusion matrix, we can see that the most misclassified images are immature granules. This makes sense because Ig cells are precursors to the other white blood cells and resemble their mature forms. Professional instrumentation also runs into similar classification issues and flags them for manual review. Current instrumentation has trouble recognizing the difference between Igs and mature cells.


The main suggestions for further research are to use the full-sized images (224 x 224) instead of scaling them down. Due to memory constraints this was not an option when performing data analysis. Using full size images may remove the discrepancies between Ig cells and other types. 

Also transforming the images in various ways to create a more robust data set could improve modeling. 


Image sources could influence modeling too. Using images sourced from the same microscope camera, slides, and stain decrease sample variation. If this model was to be used for diagnosis it would have to specify the microscope, stain and slide types it is compatible with. The model could be more marketable if it can show accurate results when testing cellular data from other microscope types, not just the CellaVision.
