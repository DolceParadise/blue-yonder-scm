# blue-yonder-scm

### Premise

This project is a part of the IIT BHU's (Team 14) Gold Medal Winning [Presentation [video]]( https://youtu.be/xict7OX1c5Y?t=8631) for the Blue Yonder Supply Chain Event at the Inter IIT Tech Meet 10.0 2022 organized by IIT Kharagpur. The problem statement demanded a solution that can decreasing carbon footprint due to rising last mile logistics and packaging as a result of increasing popularity of E-Commerce platforms during and post-Covid era. Our idea was to implement IIM Ahmedabad working paper titled [Learning to Play the Box-Sizing Game: A Machine Learning Approach for Solving the E-commerce Packaging Problem](http://vslir.iima.ac.in:8080/jspui/bitstream/11718/25489/1/34.pdf)

### Data Gathering and Preprocessing

We used the [dataset](https://storage.googleapis.com/kaggle-data-sets/55151/2669146/compressed/olist_products_dataset.csv.zip?X-Goog-Algorithm=GOOG4-RSA-SHA256&X-Goog-Credential=gcp-kaggle-com%40kaggle-161607.iam.gserviceaccount.com%2F20220705%2Fauto%2Fstorage%2Fgoog4_request&X-Goog-Date=20220705T173259Z&X-Goog-Expires=259199&X-Goog-SignedHeaders=host&X-Goog-Signature=500bff23236e7c2129cea731f9f0a266f84d90f5632899f803d60628ac7f6ea7cf61964c4922976e0249e7d912e9dbd0171c3c6b883049992dd29539532274fe67ee5f32aa71f986f3e8b593800700a624aad3a73b1edfe53abce994bf326dcda387b47da9ddb8db8dc706828b85319aaf7856f5d74caac0b66611c2c466f33bba07608b851e652e7f5410b216719c20dbe8c01a43b11fe4ea61e4a406398233d823363269dc8679076c351bb3e74dc578e9ac63381ce151a418b98a6c0f5344d8281c69f9dcb1676212253ccd7c09809e4b59bdd0b7908b0a4ab3ff6cff4e028eaca9a3e68502bdfdfeb0ed48cfb6b81850f0699bd744365f717b378a553b87) from the [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) at Kaggle. Luckily the data we used had just two NaN values which I eliminated. 

### Visualization 

I utilized the mpl_toolkits.mplot3d library to make 3D plots of the data. The idea was to visualize the products based on varying height, width and length to better grasp the importance of clustering the products into separate volume segments for the predicting the most optimized carton size. 

- <u>Unclustered Data</u> 

![unclustered_data.png](https://github.com/DolceParadise/blue-yonder-scm/blob/main/unclustered_data.png?raw=true)

- <u>After Clustering into 15 Segments</u> 

![Clustered Data](https://github.com/DolceParadise/blue-yonder-scm/blob/main/clustered_data.png?raw=true)

### Clustering

I utilized k-means clustering to cluster the dataset into 1000 clustersf for a dataset of 30,000 products through these lines of code. 

```python
kmeans = KMeans(*n_clusters*=1000, *random_state*=0).fit(dfa)
labels = kmeans.labels_
dfa_wth_std = pd.DataFrame(*data* = dfa, *columns* = ['product_height_cm','product_length_cm','product_width_cm'])
dfa_wth_std['label_kmeans'] = labels
```

### Results

This implementation was able to **increase truck spare volume by 20%**. The packaging factors was able to **increase from 0.4 to 05** because of carton optimization. Further detailed discussion of the financials of this implemention can be found on the Carton Optimization sheet of this [spreadsheet](https://docs.google.com/spreadsheets/d/1cxen6BT6lYdcLjwK445dsWggau86Mp4iqOsXr95o3pE/edit?usp=sharing). 

