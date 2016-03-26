Supervised learning
-------------------
Supervised learning is the machine learning task of inferring a function from labeled training data.

Python libraries that can be used for supervised learning
---------------------------------------------------------
http://scikit-learn.org/


### Creating a [classifier](http://scikit-learn.org/stable/modules/naive_bayes.html) fit given featureset and labels for the features
```
def classify(features_train, labels_train):   
    ### import the sklearn module for GaussianNB
    from sklearn.naive_bayes import GaussianNB
    ### create classifier
    clf = GaussianNB()
    ### fit the classifier on the training features and labels
    clf_fit = clf.fit(features_train, labels_train)
    ### return the fit classifier
    return clf_fit
```

### Checking the [accuracy](http://scikit-learn.org/stable/modules/generated/sklearn.metrics.accuracy_score.html) of the classifier 
```
def NBAccuracy(features_train, labels_train, features_test, labels_test):
    """ compute the accuracy of your Naive Bayes classifier """
    ### import the sklearn module for GaussianNB
    from sklearn.naive_bayes import GaussianNB

    ### create classifier
    clf = GaussianNB()

    ### fit the classifier on the training features and labels
    clf.fit(features_train,labels_train)

    ### use the trained classifier to predict labels for the test features
    pred = clf.predict(features_test)
    
    from sklearn.metrics import accuracy_score
    ### calculate and return the accuracy on the test data
    ### this is slightly different than the example, 
    ### where we just print the accuracy
    ### you might need to import an sklearn module
    accuracy = accuracy_score(labels_test, pred)
    return accuracy
```
