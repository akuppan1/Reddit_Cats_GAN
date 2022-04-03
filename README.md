# Reddit_Cats_GAN
Webscraping Cats and Generating pictures using a Pytorch Neural Net</br></br>
I had a simple idea. Make some artificial cat pictures.</br>
The project’s goals were the following.</br></br>
Scrape photos of cats from Reddit</br>
Create a GAN (Generative Adversarial Network)</br>
Create artificial pictures of cats!</br>
“Simple enough” I told myself... Lets dive in.</br>
3 hours later:</br></br>

Chaos</br></br>
The steps evolved into the following:</br>
Scrape Reddit using pre-existing free tools. I used Parsehub.</br>
Take scraped image urls and use another chrome extension to download all the images in the first 5 pages of /r/Cats.</br>
Upload scraped photos into a kaggle dataset. Connect dataset to kaggle notebook</br>
Locate a pre-existing Kaggle notebook of a GAN and *fingers crossed* wrangle said notebook to fit my data and generate images.</br>
So, I did the following:</br></br>
STEPS 1 and 2:</br></br>

First I used Parsehub and their wonderful tutorial video to scrape images.</br>
Parsehub’s tutorial: https://www.youtube.com/watch?v=va_sLksriOw</br>

Obtain list of image urls using Parsehub scraper</br>

Download images to my local download folder using “Tab Save” extension</br>

Viola. My Downloads folder is filled with cats!</br>
STEP 3: Create a new dataset on Kaggle with all the photos I downloaded
</br>
STEP 4:</br>
Huge shoutout to https://www.kaggle.com/ryo1993</br>
Sir, your kaggle notebook was hard to work with. I could not read Japanese, but the code was in English and it made sense to me.</br>
His GAN notebook: https://www.kaggle.com/code/ryo1993/cat-gan</br>
Kaggle fortunately had a cat repository with pre-cut images to perfection which made the GAN spit out better pictures. What came out of my notebook’s GAN was atrocious.</br>

So far so good</br>

Uh oh. These are the generated images. Those…are NOT cats :(</br></br>
There is an explanation for this.</br></br>
First off, the GAN created by the original guy used different versions of Pytorch which did not run properly. I had to rely on the notebook’s output and pray that it worked. I created a fresh notebook and made sure Pytorch and Numpy were installed (the kernels usually come with them pre-installed, but I wasn’t taking chances).
The original kernel code used input paths and specialized functions to manipulate a list of paths based on the previous cat dataset. Here, I had to remove that code, and create my own list which pointed to my dataset.</br></br>
There were some places in the other created functions as well which were pulling from the other dataset and I had to change that as well.</br>
I also had to make sure GPU was running on the Kaggle notebook or else I will have a bad time.</br></br>
Once this was said and done, the notebook did the following:</br></br>
Manipulate the images into a 64 by 64 size to standardize all the images that will go into the GAN.</br>
Train a model with the pictures in the dataset.</br>
Output the generated images……of what I hoped to be cats. Turned out it looked like a fuzzy 1990’s television.</br></br>
The reason this happened with the generated images could be the following:</br></br>
The clarity of the image (image resolution) was off. Maybe increase to 128 by 128 size.</br>
The cat photos from the original dataset were custom tailored to have just their faces. or just the cat itself. There was huge variation in my photos because they were from reddit. Future work here would be to have a filtration layer with my own sweat equity and obtain only the faces of the cats and re-run the notebook.</br></br>
FUTURE WORK</br></br>
Try scraping the photos using python Selenium. It took 40 minutes for Parsehub to get 73 images. I am sure I can do it faster somehow.</br>
Increase image size when inputing image into the GAN</br>
Change around the weights, create my own DCGAN using Pytorch/Keras with my own layers.</br>
Try different activation functions within the GAN, whatever is used in state of the art image GANs</br>
Dockerize everything. The whole reason I had to use Kaggle was because their notebooks were easy to use and were well integrated with all state of the art applications and libraries. My poor laptop is not. I am sure there is a middle ground here with Docker where I can pre-load all the required imports for Pytorch for image GAN and other use cases.
