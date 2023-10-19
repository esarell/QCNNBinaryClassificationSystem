# MscQuantumTech
This project focuses on using Quantum Convolution Nural Networks (QCNN) in order to determine signal for nosie for Gravitational Waves

Currently two students have looked into this uses pennylane as the main libary. This repostory is a continuation of there work.
-----------------------------------------------------------------------------------------------------------------------------------------

There are 6 main files used:
----------------------------------------------------
Benchmarking.py

QCNN_circuit.py

QCNN_run.py

Quantum_Data.py
Takes the data generated by sin_data_generator and encodes it for the quantum circit then outputs a file with the data in it.

sin_data_generator.py
This generates the sin graphs and the noisy graphs. 
Uses sigma (the variance) to decide how much nosie to add for each graph.
For the CNN this is the only data we need, for QCNN this data needs to be encoded, can be done in Quantum_data.py
Note will not work if sigma is 0.

Note previously sin_generator.py was used this has now been replaced by sin_data_generator.py replaces

Training.py

QCNN_test.py:
allow you to run previsously trained models and test them

CNN.py

CNN_test.py
-----------------------------------------------------------------------------------------------------------------------------------------
Note sin_generator.py is no longer used 

-----------------------------------------------------------------------------------------------------------------------------------------
Hyperparameters are stored:
Training.py

Currently best found hyper paramaters are
learning_rate = 0.01
batch_size = 5
epochs = 300

Epochs currently determined by "steps" in QCNN_run.py
Steps is not exactly the same as epochs, an epoch is when it runs through the whole data set the step is each step is just a different batch

For the current data file we are doing that means that 300 steps is equivalent to 10 epochs when the batch size is 25


Testing of hyper params
-----------------------------------------------------------------------------------------------------------------------------------------
How to run.
----------------------------------------------------
Run the QCNN_run.py file
Adjust the filename on line 46 of QCNN_run.py

Set up make sure you have three folders set up,
Models, Results and Data to collect the information

Models: Holds files for the parameters
Results: Holds the cost function/loss output
Data: Holds the specific split up of test and training set data so you can test without testing on seen data

Models are pickeld versions of the paramaters at that point, file naming convention works by using model + step number + C + Cost + .pkl
It will only
The data that was randomly split is also saved in the Data folder with a date corresponding to each bit of data. This is also pickeld
and saved in the Data folder
Run the CNN File:
----------------------------------------------------
To test a model run QCNN_test.py file.
This will then promt you to laoad in a model file and its subsequent data.
This data should be taken from the data folder and should be a .pkl file which corresponds to the designated model trained

This will then give you an accuracy for that against the models test set, which is unseen.

----------------------------------------------------
Data generation for QCNN
----------------------------------------------------
Use the Quantum_Data.py file
in the main function called the data generation function by 
quantum_data(variance,frequency)
variance, determines how much gaussian noise is added to the file
frequency should be a list with two values, this determines the range of frequencys of sin graphs created
This will then be ssaved in the Quantum_Data Folder so make sure this is already created
----------------------------------------------------
Data generation for CNN
----------------------------------------------------
Use sin_data_generator.py, this was previously sin_generator.py but this is no longer used.
In the main function, simply call 
sin_gen(snr,freq,length)
snr: is the variance that is used on the gausian to decided how much noise to add
frequence, a list of two values, [start frequency, last frequency]
length: how many sin graphs you want to generate.

This is used by the QCNN_Data.py file in order to help generate the QCNN data.
It currently has a fixed length 10000 on line 135