# CFA.Example
library(lavaan)
library(simsem)
loading <- matrix(0, 6, 2) #create a matrix of all 0s
loading[1:3, 1] <- NA #specify free parameters with NA
loading[4:6, 2] <- NA
loadingValues <- matrix(0, 6, 2)  
loadingValues[1:3, 1] <- 0.7  
loadingValues[4:6, 2] <- 0.7
LY <- bind(loading, loadingValues)
LY <- bind(loading, 0.7)
error.cor <- matrix(0, 6, 6)
diag(error.cor) <- 1
RTE <- binds(error.cor)
latent.cor <- matrix(NA, 2, 2) #specify a 2x2 matrix of NAs
diag(latent.cor) <- 1 #set the diagonal of the matrix to 1
RPS <- binds(latent.cor, 0.5) #Defaults to making all NA values in the matrix .5
CFA.Model <- model(LY = LY, RPS = RPS, RTE = RTE, modelType="CFA")
summary(CFA.Model)
dat <- generate(CFA.Model, 200)
out <- analyze(CFA.Model, dat)
Output <- sim(1000, n=200, CFA.Model)

