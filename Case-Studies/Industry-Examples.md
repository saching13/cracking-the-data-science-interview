Here are the list of industry examples that Chip compiles:

1. [Using Machine Learning to Predict Value of Homes On Airbnb](https://medium.com/airbnb-engineering/using-machine-learning-to-predict-value-of-homes-on-airbnb-9272d3d4739d) (Robert Chang, Airbnb Engineering & Data Science, 2017)

**Problem**: Predict Customer Lifetime Value of new listings

**ML Workflow**:

- Feature Engineering: Define relevant features using Airbnb's internal feature repository Zipline.
- Prototyping and Training: Train a model prototype using scikit-learn.
- Model Selection and Validation: Perform model selection and validation using various AutoML frameworks.
- Productionization: Take the selected model prototype to production using Airbnb's notebook translation framework ML Automator into an Airflow ML pipeline.

2. [Using Machine Learning to Improve Streaming Quality at Netflix](https://medium.com/netflix-techblog/using-machine-learning-to-improve-streaming-quality-at-netflix-9651263ef09f) (Chaitanya Ekanadham, Netflix Technology Blog, 2018)

**Problem**: Use ML to improve streaming quality and adapt to different/fluctuating conditions (networks and devices with widely varying capabilities)

- **Network Quality Characterization and Prediction**:
	- Can we predict what throughput will look like in the next 15 minutes given the last 15 minutes of data?
	- How can we incorporate longer-term historical information about the network and device?
	- What kind of data can we provide from the server that would allow the device to adapt optimally?
	- Even if we cannot predict exactly when a network drop will happen, can we at least characterize the distribution of throughput that we expect to see given historical data?
- **Video Quality Adaptation During Playback**:
	- Can we leverage data to determine the video quality that will optimize the quality of experience?
	- The quality of experience can be measured in several ways, including the initial amount of time spent waiting for video to play, the overall video quality experienced by the user, the number of times playback paused to load more video into the buffer ("rebuffer"), and the amount of perceptible fluctuation in quality during playback.
	- These metrics can trade off with one another. This "credit assignment" problem is a well-known challenge when learning optimal control algorithms, and ML techniques have great potential to tackle these issues.
- **Predictive Caching**:
	- Predicting what a user will play in order to cache it on the device before the user hits play, enabling the video to start faster and/or at a higher quality.
	- By combining various aspects of their viewing history together with recent user interactions and other contextual variables, one can formulate this as a supervised learning problem where we want to maximize the model's likelihood of caching what the user actually ended up playing, while restricting constraints around resource usage coming from the cache size and available bandwidth.
- **Device Anomaly Detection**:
	- Netflix has history on alerts that were triggered as well as the ultimate determination of whether or not device issues were in fact real and actionable. The data can then be used to train a model that can predict the likelihood that a given set of measured conditions constitutes a real problem.
	- It's challenging to determine the root cause of a problematic issue. Statistical modeling can help by controlling for various covariates.

3. [150 Successful Machine Learning Models: 6 Lessons Learned at Booking.com](https://blog.acolyer.org/2019/10/07/150-successful-machine-learning-models/) (Bernardi et al., KDD, 2019).

- **Different types of model**: The models deployed at Booking.com can be grouped into six broad categories:
	- **Traveller preferences models** operate in the semantic layer, and make broad predictions about user preferences (e.g., degree of flexibiilty).
	- **Traveller context models**, also semantic, which predictions about the context in which a trip is taking place (e.g. with family, with friends, for business, …).
	- **Item space navigation models** which track what a user browses to inform recommendations both the the user’s history and the catalog as a whole.
	- **User interface optimisation models** optimise elements of the UI such as background images, font sizes, buttons etc. Interestingly here, “we found that it is hardly the case that one specific value is optimal across the board, so our models consider context and user information to decide the best user interface.”
	- **Content curation models** curate human-generated content such as reviews to decide which ones to show
	- **Content augmentation models** compute additional information about elements of a trip, such as which options are currently great value, or how prices in an area are trending.

- **Lesson 1: projects introducing machine learned models deliver strong business value**
	- All of these families of models have provided business value at Booking.com. Moreover, compared to other successful projects that have been deployed but did not use machine learning, the machine learning based projects tend to deliver higher returns.
	- Once deployed, beyond the immediate business benefit they often go on to become a foundation for further product development.
- **Lesson 2: model performance is not the same as business performance**
	- An interesting finding is that increasing the performance of a model does not necessarily translate into a gain in [business] value.
	- This could be for a number of reasons including saturation of business value (there’s no more to extract, whatever you do); segment saturation due to smaller populations being exposed to a treatment (as the old and new models are largely in agreement); over-optimisation on a proxy metric (e.g. clicks) that fails to convert into the desired business metric (e.g. conversion); and the uncanny valley effect.
- **Lesson 3: be clear about the problem you’re trying to solve**
	- Before you start building models, it’s worth spending time carefully constructing a definition of the problem you are trying to solve. The Problem Construction Process takes as input a business case or concept and outputs a well-defined modeling problem (usually a supervised machine learning problem), such that a good solution effectively models the given business case or concept.
	- Some of the most powerful improvements come not from improving a model in the context of a given setup, but changing the setup itself. For example, changing a user preference model based on click data to a natural language processing problem based on guest review data.
- **Lesson 4: prediction serving latency matters**
	- In a experiment introducing synthetic latency, Booking.com found that an increase of about 30% in latency cost about 0.5% in conversion rates “a relevant cost for our business“. This is particularly relevant for machine learned models since they require significant computational resources when making predictions. Even mathematically simple models have the potential of introducing relevant latency.
	- Booking.com go to some lengths to minimise the latency introduced by models, including horizontally scaled distributed copies of models, a in-house developed custom linear prediction engine, favouring models with fewer parameters, batching requests, and pre-computation and/or caching.
- **Lesson 5: get early feedback on model quality**
	- When models are serving requests, it is crucial to monitor the quality of their output but this poses at least two challenges: (1) Incomplete feedback due to the difficulty of observing true labels; and (2) Delayed feedback e.g. a prediction made at time of booking as to whether a user will leave a review cannot be assessed until after the trip has been made.
	- One tactic Booking.com have successfully deployed in these situations with respect to binary classifiers is to look at the distribution of responses generated by the model.
- **Lesson 6: test the business impact of your models through randomised controlled trials**
	- The paper includes suggestions for how to set up the experiments under different circumstances.
	- When not all subjects are eligible to be exposed to a change (e.g., they don’t have a feature the model requires), create treatment and non-treatments groups from within the eligible subset.
	- If the model only produces outputs that influence the user experience in a subset of cases, then further restrict the treatment and non-treatment groups to only those cases where the model produces a user-observable output (which won’t of course be seen in the non-treatment group). To assess the impact of performance add a third control group where the model is not invoked at all.
	- When comparing models we are interested in situations where the two models disagree, and we use as a baseline a control group that invokes the current model (assuming we’re testing a current model against a candidate improvement).

4. [How we grew from 0 to 4 million women on our fashion app, with a vertical machine learning approach](https://medium.com/hackernoon/how-we-grew-from-0-to-4-million-women-on-our-fashion-app-with-a-vertical-machine-learning-approach-f8b7fc0a89d7) (Gabriel Aldamiz, HackerNoon, 2018)

- **Thesis**: Outfits are the best asset to understand people’s taste. Understanding taste will transform online fashion. The Fashion Taste API builds a Taste Graph for each fashion retailer, their system of intelligence to understand why a shopper buys a product. It’s a strategic asset that includes Taste Profiles, a fashion ontology, and our own interpretation of fashion products.
- **1st Step: Building the app for people to express their needs** - Three things helped with retention:
	- (a) identify retention levers using behavioral cohorts.
	- (b) re-think the onboarding process, once we knew the levers of retention.
	- (c) define how we learn.
- **2nd step: Building the data platform to learn people’s fashion needs**
	- Social Fashion Graph is a compact representation of how needs, outfits and people interrelate, a concept that helped us build the data platform. The data platform creates a high-quality dataset linked to a learning and training world, our app, which therefore improves with each new expression of taste.
	- We ended up opening up this technology to fashion retailers, with the Fashion Taste API. The objective of the Fashion Taste API is to empower teams to own taste data from each of their shoppers, so they can built memorable experiences for their clients. Truly effective fitting room smart mirrors, in-store fashion stylists, and personalized omnichannel experiences.
	- We thought of outfits as playlists: an outfit is a combination of items that makes sense to consume together. Using collaborative filtering, the relations captured here allow us to offer recommendations in different areas of the app.
- **3rd Step: Algorithms**
	- Fashion has its own challenges.
	- There is not an easy way to match an outfit to a shoppable product (think about most garments in your wardrobe, most likely you won’t find a link to view/buy those garments online, something you can do for many other products you have at home). Another challenge: the industry is not capturing how people describe clothes or outfits, so there is a strong disconnect between many ecommerces and its shoppers. Another challenge: style is complex to capture and classify by a machine.
	- Owning the correct data set allows us to focus on the specific narrow use cases related to outfit recommendations, and to focus on delivering value through the algorithms instead of spending time collecting and cleaning data. People’s very personal style can become as actionable as metadata and possibly as transparent as well (?), and I think we can see the path to get there. As we have a consumer product that people already love, we can ship early results of these algorithms partially hidden, and increase their presence as feedback improves results.

5. [Machine Learning-Powered Search Ranking of Airbnb Experiences](https://medium.com/airbnb-engineering/machine-learning-powered-search-ranking-of-airbnb-experiences-110b4b1a0789) (Mihajlo Grbovic, Airbnb Engineering & Data Science, 2019)



6. [From shallow to deep learning in fraud](https://eng.lyft.com/from-shallow-to-deep-learning-in-fraud-9dafcbcef743) (Hao Yi Ong, Lyft Engineering, 2018)



7. [Space, Time and Groceries](https://tech.instacart.com/space-time-and-groceries-a315925acf3a) (Jeremy Stanley, Tech at Instacart, 2017)



8. [Uber's Big Data Platform: 100+ Petabytes with Minute Latency](https://eng.uber.com/uber-big-data-platform/) (Reza Shiftehfar, Uber Engineering, 2018)



9. [Creating a Modern OCR Pipeline Using Computer Vision and Deep Learning](https://blogs.dropbox.com/tech/2017/04/creating-a-modern-ocr-pipeline-using-computer-vision-and-deep-learning/) (Brad Neuberg, Dropbox Engineering, 2017)



10. [Scaling Machine Learning at Uber with Michelangelo](https://eng.uber.com/scaling-michelangelo/) (Jeremy Hermann and Mike Del Balso, Uber Engineering, 2019)
