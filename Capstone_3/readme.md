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


All images were resized to 64 x 64 pixels. A grey scale and RBG image resized set was created. The images were then made into arrays, flattened, and scaled by dividing by 255. These arrays were saved in pandas data frame labeled with their respective cell type.
Two data frames were made, one for grey scale images and one for RBG images.


### Modeling


A K nearest neighbor model was created with the gray scale data set. Optimal KNN was found to be 15. The model evaluation can be seen below.


	Precision	Recall	f1-score
Ig	        0.52	0.25	0.34
basophil	0.52	0.45	0.48
eosinophil	0.4	    0.84	0.54
lymphocyte	0.78	0.79	0.78
monocyte	0.43	0.55	0.48
neutrophil	0.89	0.31	0.46
accuracy			0.51
macro avg	0.59	0.53	0.51
weighted avg	0.6	0.51	0.49


Because of poor performance no more modeling was preformed on the gray scale data frame.


A K nearest neighbor model was created with the RBG data set. Optimal KNN was found to be 12. The model evaluation can be seen below.
 
 
 
RBG KNN	Precision	Recall	f1-score	AUC
Ig	        0.62	0.26	0.36	0.44
basophil	0.6	    0.31	0.41	0.53
eosinophil	0.43	0.88	0.58	0.39
lymphocyte	0.72	0.84	0.77	0.96
monocyte	0.43	0.63	0.51	0.87
neutrophil	0.89	0.42	0.57	0.91
accuracy			0.54	
macro avg	0.62	0.56	0.45	
weighted avg	0.63	0.54	0.53	


The RBG images performed better than the gray scale. But still not the best results.


A random forest model was created using the RBG data set, seen below.
 
 
RBG Random Forest	Precision	Recall	f1-score	AUC
Ig	        0.61	0.8	    0.69	0.42
basophil	0.75	0.42	0.54	0.67
eosinophil	0.88	0.93	0.9	    0.35
lymphocyte	0.87	0.81	0.84	0.98
monocyte	0.87	0.39	0.54	0.95
neutrophil	0.86	0.95	0.9	    0.99
accuracy			0.79	
macro avg	0.81	0.72	0.74	
weighted avg	0.8	0.79	0.78	


The random forest model performs significantly better than the KNN.


A Tensor flow model was created using the RBG data frame. Its results are below.

	  
Tensor Flow	Precision	Recall	f1-score	AUC
Ig	        0.65	0.49	0.56	0.88
basophil	0.62	0.63	0.62	0.94
eosinophil	0.91	0.8	    0.85	0.96
lymphocyte	0.81	0.82	0.81	0.98
monocyte	0.55	0.79	0.65	0.94
neutrophil	0.81	0.91	0.85	0.97
accuracy			0.74	
macro avg	0.72	0.74	0.72	
weighted avg	0.75	0.74	0.74	
5-k fold mean accuracy	0.6239			

It performed significantly better than all other models as can easily be seen when comparing the AUCs. However, the k fold test does not match the overall model statistics.
A grid search was performed on the TensorFlow model returning the best accuracy score of 0.79. The best parameters were the following:
•	Batch size: 20
•	Dropout rate: 0.1
•	Epochs: 40
•	Learning rate: 0.0005 
•	Nodes: 32


Using these parameters our final tensor flow model statistics were calculated.


Tensor Flow Grid Search	Precision	Recall	f1-score	AUC
Ig	        0.79	0.3	    0.4	    0.91
basophil	0.44	0.84	0.58	0.95
eosinophil	0.89	0.93	0.91	0.99
lymphocyte	0.84	0.81	0.83	0.98
monocyte	0.54	0.9	    0.67	0.96
neutrophil	0.92	0.83	0.87	0.98
accuracy			0.74	
macro avg	0.74	0.77	0.72	
weighted avg	0.79	0.74	0.73	
5-k fold mean accuracy	0.7881			


The grid search parameters fixed the k fold discrepancy. It also increased the AUC for all cell types. This model was chosen as the best model for this project based on its statistics. Also, image processing works better with neuronets. 


### Discussion


The final model created from this analysis performs very well. It has high AUC scores across the six chosen cell types, and an overall accuracy around 0.79.  Looking at the confusion matrix, we can see that the most misclassified images are immature granules. This makes sense because Ig cells are precursors to the other white blood cells and resemble their mature forms. Professional instrumentation also runs into similar classification issues and flags them for manual review. Current instrumentation has trouble recognizing the difference between Igs and mature cells. Also, eosinophils are sometimes typed as neutrophils. This is an ongoing issue in hematology analyzers.
The main suggestions for further research are to use the full-sized images (224 x 224) instead of scaling them down. Due to memory constraints this was not an option when performing data analysis. Using full size images may remove the discrepancies between Ig cells and other types. Also transforming the images in various ways to create a more robust data set could improve modeling. 
Image sources could influence modeling too. Using images sourced from the same microscope camera, slides, and stain decrease sample variation. If this model was to be used for diagnosis it would have to specify the microscope, stain and slide types it is compatible with. The model could be more marketable if it can show accurate results when testing cellular data from other microscope types, not just the CellaVision.

