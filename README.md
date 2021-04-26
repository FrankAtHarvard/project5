	My approach to creating this model evolved over several iterations and several days of testing on different size datasets with various configurations.
For the Conv2d filters, 32 filters seemed to be the best fit. I experimented with lower and higher number of filters however no change in loss or 
increase in accuracy. The kernel size of 3x3 was also ideal specification. Adding a 2nd convolutional input layer with max pooling
of 2x2 increased accuracy and minimized loss over the default. I also experimented with bias initializers using HeNormal(), RandomNormal()
and Zeros(). Experimentation showed that HeNormal bias strategy without any seeding lowered loss and provided for higher accuracy  over the default glorot_uniform.

	I added two hidden layers with 128 nodes each which had a dramatic impact on minimizing loss and the rate of accuracy climbed
higher, faster in earlier epoch's. I experimented with differing node sizes of the hidden layers however 128 seemed to perform best. The model
also seemed to perform well when the hidden layers were of the same size. Additionally, I decreased the dropout rate to 20% given 
the size of the hidden layers and this seemed to provide more consistent accuracy overall between executions. Most interesting of all was
changing the activation function to sigmoid. When I made this change, the model consistently scored 97-98% accuracy with a loss averaging
around 0.07 as indicated in the run below. However, since sigmoid activation is not the preferred activation function for most 
of today's applications I set my code back to use ReLu which does not perform as accurate or as well as sigmoid. The sigmoid activation function
does take slightly longer to execute training. I also worried about saturation and the vanishing gradient issues with sigmoid which I may have seen
on some of the executions since the results would at times be no better than ReLu activation and the loss would grow unexpectedly higher at times.
	
	Finally, I cannot explicitly confirm this behavior however it seemed that on subsequent runs the images were cached and the model tended 
to do worse versus executing with an empty cache. Furthermore, I converted the images to grayscale to verify if this would impact training and accuracy but 
this change had no noticeable impact.

Sigmoid:
Epoch 1/10
500/500 [==============================] - 7s 13ms/step - loss: 3.3559 - accuracy: 0.1052
Epoch 2/10
500/500 [==============================] - 6s 13ms/step - loss: 1.8376 - accuracy: 0.4045
Epoch 3/10
500/500 [==============================] - 7s 13ms/step - loss: 1.2190 - accuracy: 0.6221
Epoch 4/10
500/500 [==============================] - 6s 13ms/step - loss: 0.5825 - accuracy: 0.8532
Epoch 5/10
500/500 [==============================] - 7s 13ms/step - loss: 0.3024 - accuracy: 0.9313
Epoch 6/10
500/500 [==============================] - 7s 13ms/step - loss: 0.1815 - accuracy: 0.9616
Epoch 7/10
500/500 [==============================] - 7s 13ms/step - loss: 0.1485 - accuracy: 0.9649
Epoch 8/10
500/500 [==============================] - 7s 13ms/step - loss: 0.1060 - accuracy: 0.9770
Epoch 9/10
500/500 [==============================] - 7s 13ms/step - loss: 0.0787 - accuracy: 0.9826
Epoch 10/10
500/500 [==============================] - 7s 13ms/step - loss: 0.0677 - accuracy: 0.9854
333/333 - 1s - loss: 0.0716 - accuracy: 0.9802

ReLu with HeNormal() bias initializer:
Epoch 1/10
500/500 [==============================] - 6s 12ms/step - loss: 4.2143 - accuracy: 0.2448
Epoch 2/10
500/500 [==============================] - 6s 12ms/step - loss: 0.8727 - accuracy: 0.7350
Epoch 3/10
500/500 [==============================] - 6s 12ms/step - loss: 0.3984 - accuracy: 0.8800
Epoch 4/10
500/500 [==============================] - 6s 12ms/step - loss: 0.2589 - accuracy: 0.9256
Epoch 5/10
500/500 [==============================] - 6s 12ms/step - loss: 0.2037 - accuracy: 0.9409
Epoch 6/10
500/500 [==============================] - 6s 12ms/step - loss: 0.1589 - accuracy: 0.9564
Epoch 7/10
500/500 [==============================] - 6s 12ms/step - loss: 0.1093 - accuracy: 0.9675
Epoch 8/10
500/500 [==============================] - 6s 12ms/step - loss: 0.1726 - accuracy: 0.9538
Epoch 9/10
500/500 [==============================] - 6s 12ms/step - loss: 0.1214 - accuracy: 0.9652
Epoch 10/10
500/500 [==============================] - 6s 12ms/step - loss: 0.1187 - accuracy: 0.9704
333/333 - 1s - loss: 0.1403 - accuracy: 0.9675