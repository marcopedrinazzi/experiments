# FML

Standard machine learning approaches require centralizing the training data into a common store.
So let's say we want to train a keyboard prediction model based on user interactions.
Traditionally, we implemented intelligence by collecting all the data on the server, create a model, and then serve it.
Clients all talk to the server to make prediction. **The model and the data is all in one central location, making it extremely easy.**
But **the downside** of this centralized setup is that this back-and-forth communication can hurt the user experience due to network latency, connectivity, battery lives, and all sorts of unpredictable issues.
**One way to solve this** is to have each client independently train its own model using its own data right on the device. No communication necessary. Great idea, right?
Well, not quite because each individual device does not have enough data to render a good model. You could pre-train the model on the server and then deploy it. But the problem with that is, in our smart keyboard example, let's say if everyone started using a new trendy word today, then the model trained on yesterday's data won't be as useful.
So what should we do to utilize the goodness of decentralized data while maintaining users' privacy?
Well, that's where federated learning comes in.
**The core idea behind federated learning is decentralized learning, where the user data is never sent to a central server.**
So how does it work?
Well, you start with a model on the server, distribute it to the clients.
But you can't just deploy to every client because you don't want to break the user experience.
You will identify these clients based on which ones are available, plugged in, and not in use.
Then, also find out which ones are suitable because not all clients will have the sufficient data.
Once you've identified suitable devices, we can then deploy the model to them.
Now, each client trains the model locally using its own local data and produces a new model, which is sent to the server.
The thing to know here is that the data used to train the model on the individual device never leaves the device.
Only the weights, biases, and other parameters learned by the model leave the device.
The server then gets all the locally trained models and averages them out, effectively creating a new master model.
**But how do we know that this process is doing something meaningful and actually creating a good model?**
Doing this once is not enough. We have to do it over and over so the combined model becomes the initial model for the next round.
And with every round, the combined model gets a little bit better thanks on the data from all those clients.
And many, many rounds later, your smart keyboard begins to show signs of intelligence.
Now, we just saw that all the training data remains on your device and no individual updates are stored in the cloud.
**For additional privacy in federated learning**, we can use the concept of **secure aggregation**, where the server pairs up devices with others in a buddy system. For example, here, each device has two buddies. Data from each device can be combined with the random values before being sent to the server. The server obviously knows the value sent to the buddies and cancels them out to just get the payload. **This trick obfuscates the data while in transit to the server.**
If you've used Google Keyboard, the Gboard, then you have already seen and experienced a federated learning use case.
The Gboard shows a suggested query, your phone locally stores information about the current context and whether you clicked the suggestion.
Federated learning processes that history on device to suggest improvements to the next iteration of Gboard's query suggestion model.
In this episode, we learned that federated learning is a collaborative and decentralized approach to machine learning that allows for smarter models, lower latency, and less power consumption, all while ensuring user privacy.
Federated learning is still a relatively new concept, and there's definitely more to come in the future.

**https://www.tensorflow.org/federated**

# Contributions to Decentralized and Privacy-Preserving Machine Learning
**http://researchers.lille.inria.fr/abellet/papers/HDR.pdf**

This stands in contrast to the fact that data is inherently decentralized in many use-cases of ML: medical data is collected by several hospitals, consumer data is collected by different companies, user data is generated by personal devices, etc. Collecting and storing data from multiple parties on a central server can incur high communication and infrastructure costs, and may not even be feasible in data-intensive applications.
more crucially, centralized ML assumes the existence of a trusted curator who securely collects, stores and processes the raw data. As modern devices collect ever more sensitive personal data (e.g., browsing/purchase logs, geolocation data, speech utterances) and privacy scandals regularly make the news, many users of digital services are looking for more privacy-preserving solutions that do not require to hand over their data to the service provider. Situations where data owners may not be willing to share their raw data also arise when keeping control of data represents a competitive advantage (e.g., in business or research), and when data sharing is restricted by legal constraints (related to intellectual property or data privacy regulations).
Decentralized learning, also known as federated learning, has recently emerged as a way to address the limitations of centralized ML. This fast-growing research area aims to allow a set of participants with local datasets to collaboratively train machine learning models while keeping their data decentralized [AB-Journal1]. Decentralized learning effectively moves most of the computation from the data center to where data is naturally located (e.g., on user devices). Like their centralized counterparts, decentralized learning algorithms are typically iterative procedures: participants update the current model in parallel using their local data, and these updates are then aggregated to form a new version of the model (McMahan et al., 2017). The aggregation step can be performed globally through communication with a central coordinator, or locally via peer-to-peer exchanges among subsets of users in the network (Lian et al., 2017).
Decentralized learning comes with its own set of challenges, which are distinct from those arising in traditional parallel/distributed ML designed to run in a cluster environ- ment (see e.g., Bekkerman et al., 2011). I highlight here two main challenges (see the survey [AB-Journal1] for a more complete discussion). First and foremost, local datasets exhibit large heterogeneity as they reflect the usage and production patterns specific to each participant. In other words, they are not independent and identically distributed (non-IID). Intuitively, this makes decentralized learning harder because participants may largely disagree about how the model should be updated (Karimireddy et al., 2020). An important challenge is then to design decentralized algorithms that can solve a variety of ML tasks on highly heterogeneous local datasets, while operating under low communi- cation budget and scaling gracefully with the number of participants.
**A second challenge in decentralized learning is related to protecting the privacy of par- ticipants with respect to other parties.** Avoiding to share raw data is a good starting point to design privacy-preserving solutions but is not sufficient to obtain robust privacy guarantees. In centralized ML, where a trusted curator only releases the trained model, information about individual training data points can be extracted from the model or its predictions (Shokri et al., 2017). This information can turn out to be very sensitive, as illustrated for instance by my work on reconstructing genotypes in private genomic databases from genetic risk score models [AB-Conf6]; [AB-Journal2]. Compared to the centralized setting, decentralized ML provides an additional attack surface as participants get to observe intermediate model updates instead of only the final model (Nasr et al., 2019). A key challenge is thus to design decentralized algorithms with rigorous privacy guarantees, minimizing the impact on the utility (accuracy) of the resulting models.
To summarize, it is crucial to design ML algorithms that can learn from heterogeneous decentralized datasets under rigorous privacy requirements, and to formally character- ize the underlying trade-offs between utility, privacy, and efficiency. This manuscript presents some of my contributions towards achieving this goal.


# Sonia's Talk FIT Milan
In classical ML data is collected on the users' devices. Data is sent to a remote infrastructure. A ML model is trained. To get predicitons, the user is granted access locally or remotely to the trained model. **BUT** sending data may be too costly. Data may be considered too sensitive. The central server may be subject to failures. Scaling the central server with an increasing number of clients may be costly.
1. Model initialization
2. Local training (clients)
3. Model aggregation (solo i parametri) (central server) 
4. Il modello aggregato ?? inviato indietro al client e il tutto si ripete

FL key charateristics: data is generated locally, data is imbalanced and not independent and identically distributed. Privacy/Robustness constraints: model updates may embedd knowledge about the participants, limited reliability/availability of participants, robustness against selfish parties, robustness against malicious parties

Cross-silo vs Cross-device FL. Server Ochestrated vs Fully Decentralized FL.

[.........]