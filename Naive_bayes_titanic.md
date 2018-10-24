

```R
library('e1071')
data('Titanic')
```


```R
Titanic_df = as.data.frame(Titanic)
```


```R
head(Titanic_df)
```


<table>
<thead><tr><th scope=col>Class</th><th scope=col>Sex</th><th scope=col>Age</th><th scope=col>Survived</th><th scope=col>Freq</th></tr></thead>
<tbody>
	<tr><td>1st   </td><td>Male  </td><td>Child </td><td>No    </td><td> 0    </td></tr>
	<tr><td>2nd   </td><td>Male  </td><td>Child </td><td>No    </td><td> 0    </td></tr>
	<tr><td>3rd   </td><td>Male  </td><td>Child </td><td>No    </td><td>35    </td></tr>
	<tr><td>Crew  </td><td>Male  </td><td>Child </td><td>No    </td><td> 0    </td></tr>
	<tr><td>1st   </td><td>Female</td><td>Child </td><td>No    </td><td> 0    </td></tr>
	<tr><td>2nd   </td><td>Female</td><td>Child </td><td>No    </td><td> 0    </td></tr>
</tbody>
</table>




```R
repeating_sequence=rep.int(seq_len(nrow(Titanic_df)), Titanic_df$Freq)
Titanic_dataset=Titanic_df[repeating_sequence,]
row.names(Titanic_dataset) = NULL
Titanic_dataset$Freq=NULL
head(Titanic_dataset)
```


<table>
<thead><tr><th scope=col>Class</th><th scope=col>Sex</th><th scope=col>Age</th><th scope=col>Survived</th></tr></thead>
<tbody>
	<tr><td>3rd  </td><td>Male </td><td>Child</td><td>No   </td></tr>
	<tr><td>3rd  </td><td>Male </td><td>Child</td><td>No   </td></tr>
	<tr><td>3rd  </td><td>Male </td><td>Child</td><td>No   </td></tr>
	<tr><td>3rd  </td><td>Male </td><td>Child</td><td>No   </td></tr>
	<tr><td>3rd  </td><td>Male </td><td>Child</td><td>No   </td></tr>
	<tr><td>3rd  </td><td>Male </td><td>Child</td><td>No   </td></tr>
</tbody>
</table>




```R
Naive_Bayes_Model=naiveBayes(Survived ~., data=Titanic_dataset)
```


```R
Naive_Bayes_Model
```


    
    Naive Bayes Classifier for Discrete Predictors
    
    Call:
    naiveBayes.default(x = X, y = Y, laplace = laplace)
    
    A-priori probabilities:
    Y
          No      Yes 
    0.676965 0.323035 
    
    Conditional probabilities:
         Class
    Y            1st        2nd        3rd       Crew
      No  0.08187919 0.11208054 0.35436242 0.45167785
      Yes 0.28551336 0.16596343 0.25035162 0.29817159
    
         Sex
    Y           Male     Female
      No  0.91543624 0.08456376
      Yes 0.51617440 0.48382560
    
         Age
    Y          Child      Adult
      No  0.03489933 0.96510067
      Yes 0.08016878 0.91983122




```R
NB_Predictions=predict(Naive_Bayes_Model,Titanic_dataset) 
Titanic_dataset$NB_Pred = NB_Predictions
```


```R
summary(Titanic_dataset)
```


      Class         Sex          Age       Survived   NB_Pred   
     1st :325   Male  :1731   Child: 109   No :1490   No :1726  
     2nd :285   Female: 470   Adult:2092   Yes: 711   Yes: 475  
     3rd :706                                                   
     Crew:885                                                   



```R
table(Titanic_dataset$Age , Titanic_dataset$NB_Pred , Titanic_dataset$Sex)
```


    , ,  = Male
    
           
              No  Yes
      Child   59    5
      Adult 1667    0
    
    , ,  = Female
    
           
              No  Yes
      Child    0   45
      Adult    0  425


