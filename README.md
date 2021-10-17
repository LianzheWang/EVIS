# Evolving-Image-Search (EVIS) Dataset

In our paper "Active Gradual Domain Adaptation: Dataset and Approach", to evaluate the model performance on web applications with gradual domain drift, we use an automatic approach to construct a new Evolving-Image-Search (EVIS) dataset. EVIS consists of real-world web images that appeared in Google image search results.

## How to Use EVIS Dataset
The whole dataset could be downloaded directly from this repository. You may also download compressed dataset from link: 

You could find example script using EVIS dataset at: 

(It is actually the implementation of our paper. Example PyTorch EVIS dataset class is included in the script. )


## Dataset Introduction
EVIS consists of real-world web images that appeared in Google image search results, with individually recorded searching keyword labels and uploading times. The collection process of EVIS is purely done automatically without any manual selection or annotation. 

There are massive image data resources on the Internet. In different years, the web images are undergoing a gradual domain shift, e.g., the ``mobile phone'' related images on the Internet have undergone drastic and continuous changes in recent years. Therefore, web images have great potential to be adopted in the research of gradual domain shift adaptation-related work. However, there is currently no existing automatic approach to construct a web image dataset for gradual domain shift learning researches. The construction work of the EVIS dataset could fill this gap to some extent.

We selected 10 objects with strong changes in this era (5 types of electronic products: mobile phone, laptop, tablet PC, television, electronic watch. 5 types of vehicles: car, van, truck, bus, taxi), use their names as keywords to search and collect on the Google image search engine. In particular, we will restrict the upload time range of the images in the search results through the API, and the length of each search interval is set to one month. For each month, We perform one set of searches, and each set of searches includes one search for each of the above keywords. To reduce the overlap and similarity of results in different searches, we prefix the search keyword with the word ``new''. We also filter out search results that are too small (less than 200×200 pixels) or too large (greater than 1500×1500 pixels). The time range for the data collection is from 2009 to 2020, as shown in Figure below.

<img src="https://user-images.githubusercontent.com/46777301/137609662-5f369055-0849-474f-a950-9a3027de8682.png" width="600" height="400">

A crawler program is developed by us to automatically complete the above searching process, at the same time download the first 40 downloadable images for each keyword searching result. The search keywords are recorded as labels each time. All downloaded images are resized to 256×256 pixels and saved in JPG format. In this way, the EVIS dataset has a total of 12×12×10×40 (years, months, categories, downloads per search) = 57600 pictures, as shown in Table below.

<img src="https://user-images.githubusercontent.com/46777301/137609784-8769741c-4d74-4b8e-a509-62d568dc3a54.png" width="400" height="125">

There could be a certain amount of noise in the dataset purely collected from the search engine, such as unrelated images that appear in the search results, as shown in Figure below. We deliberately retain this part of the noise to simulate the noise environment that the model needs to deal with in real application scenarios and to retain the fully automatic collecting property of our dataset constructing method. We tested the dataset and found that through proper training, the prediction model can predict the results of neighboring domains with 80\% accuracy while only learning limited samples. It's a decent result for such a classification task for 10 categories, showing that the EVIS dataset is with the quality of deep model learning research. 

<img src="https://user-images.githubusercontent.com/46777301/137609810-c595d081-79ee-4284-8df2-c5feb7ab7190.png" width="450" height="505">

Through experiments, we can prove the gradual domain shift characteristics of the data in the EVIS. After training the source model with part of the data from 2009 to 2011, we use it to predict the data from 2012 to 2020, and found that the prediction accuracy showed a smooth downward trend year by year, as shown in Figure below. The results of this experiment help to show that the data domain distribution in the EVIS dataset gradually shifts over time. 

<img src="https://user-images.githubusercontent.com/46777301/137609884-84620990-af0f-40f8-a941-ee73cbf754f4.png" width="450" height="266">

Furthermore, we make a study on the measurement of the degree of evolution over the last decade for the 10 selected objects. We first again use the source model trained on data before 2011 to predict data from 2012 to 2020. Then, for each year, we record the per-category accuracy. Finally, for each category, we make a linear regression for the accuracy record from 2012 to 2020, take the regression slope value as the approximation of the accuracy decreasing rate (the average amount of accuracy decrease per year for each specific category).

<img src="https://user-images.githubusercontent.com/46777301/137609895-9e8ebb05-7817-4dcc-a896-cbd54538dca7.png" width="450" height="285">

## Citation
If you find EVIS dataset helpful in your research work, please cite our work by:
