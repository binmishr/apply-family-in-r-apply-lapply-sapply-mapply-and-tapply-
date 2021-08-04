# apply-family-in-r-apply-lapply-sapply-mapply-and-tapply

apply family in r,  In this article, we are going to discuss the R Apply family. The apply family is an inbuilt R package, so no need to install any packages for the execution.

The main advantage of apply function is we can get rid of loop operations.

apply family in r contains apply(), lapply(), sapply(), mapply() and tapply().

One of the big questions is how and when to use these functions?

The answer is simple its depends on the structure of your data set and how you want the outcome.

Let’s see how to execute these functions one by one.
1. apply()

The syntax is

apply(X, MARGIN, FUN, …)

Returns a vector or array or list of values obtained by applying a function to margins of an array or matrix.

Let’s create a square matrix first and we want to evaluate the sum of each row.

mymatrix<-matrix(1:9,nrow=3)
mymatrix
[,1] [,2] [,3]
[1,]    1    4    7
[2,]    2    5    8
[3,]    3    6    9

Let’s calculate the row sum.

apply(mymatrix,1,sum)  
[1] 12 15 18

Let’s calculate the column sum

apply(mymatrix,2,sum) 
[1]  6 15 24

Let’s create NA value in the matrix and see how we can execute the function.

mymatrix[2,3]<-NA
[,1] [,2] [,3]
[1,]    1    4    7
[2,]    2    5   NA
[3,]    3    6    9
apply(mymatrix,1,sum)
[1] 12 NA 18

Insert na.rm function in the above code and see the result.

apply(mymatrix,1,sum,na.rm=TRUE)
[1] 12  7 18

This is one small example, the same way you can make use of apply() function in R.
2. lapply()

lapply(X, FUN,…)

lapply returns a list of the same length as X, each element of which is the result of applying FUN to the corresponding element of X.

lapply not required the margin. Let’s see an example for lapply.

First we need to create a list.

mylist<-list(A=matrix(1:9,nrow=3),B=1:5,C=8)
mylist
$A
     [,1] [,2] [,3]
[1,]    1    4    7
[2,]    2    5    8
[3,]    3    6    9
$B
[1] 1 2 3 4 5
$C
[1] 8

Let’s calculate the sum of each list.

lapply(mylist,sum)
$A
[1] 45
$B
[1] 15
$C
[1] 8

You can see how the results are saved as a list form. Suppose if you want vector result just unlist the same.

unlist(lapply(mylist,sum))
A  B  C
45 15  8

You can create your own functions and ppass into the function.

For example, suppose if you want multiply each element with value 20 just use the below code.

lapply(mylist,function(x) x*20)
$A
     [,1] [,2] [,3]
[1,]   20   80  140
[2,]   40  100  160
[3,]   60  120  180
$B
[1]  20  40  60  80 100
$C
[1] 160

The same way, you can utilize lapply in different cases.
3. sapply()

sapply is a user-friendly version and wrapper of lapply by default returning a vector, matrix or, if simplify = “array”, an array if appropriate, by applying simplify2array(). sapply(x, f, simplify = FALSE, USE.NAMES = FALSE) is the same as lapply(x, f).

sapply(mylist,sum)

it follows the same job in laaply instead of list this function can handle vector.

A  B  C
45 15  8

4. mapply()

maaply(FUN, …)

m stands for multi-variant apply.

Let’s take an example to suppose we have replicate values of 1 of four times and we want to replicate 1 at 4 times, 2 at 3 times, 3 at 2 times, and 4 at 1 time.

mapply(rep,1:4,4:1)
[[1]]
[1] 1 1 1 1
[[2]]
[1] 2 2 2
[[3]]
[1] 3 3
[[4]]
[1] 4

Let’s create a user-defined function and see how mapply will perform.

Suppose if we have two vectors x and y.

x<-c(A=20,B=1,C=40)
 y<-c(J=430,K=50,L=10)

Imagine if you want to add these two vectors and multiply by 2. First, create the function and pass it into mapply.

simply<-function(u,v){
  (u+v)*2
}
mapply(simply,x,y)
A   B   C 
900 102 100 

6. tapply()

Apply a function to each cell of a ragged array, that is to each (non-empty) group of values given by a unique combination of the levels of certain factors.

Let’s iris dataset for an example, suppose if we want to calculate the maximum value of sepal length for all groups.

tapply(iris$Sepal.Length,iris$Species,max)
setosa versicolor  virginica
  5.8        7.0        7.9

Conclusion

apply:- Appy function over the margins of an array.

lapply:- Loop over a list and evaluate a function on each element

sapply:- Same as lapply but try to simply the result.

mapply:- Multivariate version of lapply

tapply:-apply a function over subsets of a vector.
