---
layout: post
title:  "StephenCurry Shot Prediction"
date:   2019-02-11
excerpt: "Coding an ANN model from scratch used to predict a shot by Stephen as sucess or not"
project: true
tag:
- Python 
- Web Scraping
- Backward Propagation
- Keras
comments: true
---

![shots distribution](https://github.com/jeremite/jeremite.github.io/blob/master/assets/img/Post/curry1.png?raw=true) 

CLICK HERE:
[Notebook Version](https://github.com/jeremite/curry_shot/blob/master/stephen_shot.ipynb)<br>
CLICK HERE:
[Medium Blog for Coding](https://medium.com/deep-learning-construction/neural-network-build-from-scratch-without-frameworks-1-302dcfb46127)

## OVERVIEW
For this project, I used Beautifulsoup package to extract data from a NBA stats website regarding Stephen Curry's shot points in Season 2014-2016. With the data, I built a neural network with Adam optimizer from scratch without any frameworks or packages, to predict whether a shot made by Stephen at a specific point will succeed or not.

## DETAILS
The website I crawled hasn't updated anymore, thus I only got the stats for season 2014-2015 and 2015-2016. The pachage *beautifulsoup* is quite easy to use:
### extracting the data into JSON format
    url = 'http://buckets.peterbeshai.com/api/?player=201939&season=2015'
    data = requests.get(url, headers={
                "User-Agent": "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/50.0.2661.102 Safari/537.36"})
    cor =[]    
    made = []

    for shot in response.json():
        cor.append((shot['LOC_X'],shot['LOC_Y']))
        made.append(shot['EVENT_TYPE'])
 
The variable *cor* saved the coordinates of the positions where Stephen made shots and *made* is a binary class indicates whether he made it or not. I visualized the data into the graph shown at the top and the code is as follows:

### plot the data on top of a court image
    court_map = plt.imread('shotchart.png')
    BB = (-300, 300, -50, 400)
    def plot_data(df,BB,alpha=0.6,maps=court_map,s=10):
        fig, ax = plt.subplots(figsize=(15,10))
        #ax.scatter(df['pickup_longitude'],df['pickup_latitude'], alpha=alpha,c='r',s=s,zorder=1,marker='.')
        ax.scatter(df[0,np.where(y==1)], df[1,np.where(y==1)],zorder=2,alpha=alpha,c = 'b', s=2, cmap=plt.cm.Spectral, label='Made Shot')
        ax.scatter(df[0,np.where(y==0)], df[1,np.where(y==0)],zorder=2,alpha=alpha,c = 'r', s=2, cmap=plt.cm.Spectral, label='Miss Shot')
        ax.legend(loc=1)
        #ax.set_xlim(BB[1],BB[0])
        #ax.set_ylim(BB[3],BB[2]) 
        ax.xaxis.set_label_text('longitude')
        ax.yaxis.set_label_text('latitude')
        ax.set_title('Shooting Points')
        ax.imshow(maps, zorder=0,extent=BB)
    plot_data(x,BB)
   
### construct ANN architecture from scratch
Then, I created the ANN from scratch: built single forward propagation and backward propagation block, with repect to different activation functions (relu, sigmoid, tanh); define parameters initialization and parameters update with Adam functions; define cost function, etc. I wrote a blog about the whole coding process, please kindly [find it here.](https://medium.com/deep-learning-construction/neural-network-build-from-scratch-without-frameworks-1-302dcfb46127)

The model works well and the loss curve is placed below:
![loss curve](https://github.com/jeremite/jeremite.github.io/blob/master/assets/img/Post/curry2.png?raw=true) 
