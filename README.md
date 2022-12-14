# Quantum Spiking Neural Networks (QSpikeNN)

<img align="center" alt="diag" width="1000" height="600" src="https://github.com/adi666-png/QSpikeNN/blob/main/assets/diag.png">

The proposed hybrid classical-quantum
DSQ-Net model consists of a classical pre-trained SNN, one
dressed quantum layer for classification (whose qubits are
further measured to collapse to classical bits) and a final
classical post-processing layer for obtaining the outcomes.
Additionally, a classical pre-processing layer is employed
to connect the temporal pooling layer and the dressed quan-
tum layer of the model architecture. The brief descriptions
of different modules used in the development of DSQ-Net
are provided below.

1. ClassicalSNNGenerator.ipynb
It contains the codes to generate Spiking Neural
Networks. This file is used to make the pre-trained
network of the proposed DSQ-Net model for the
different datasets. It is a classical Sequential
model, which consists of the following:
(a). Linear Layer: It comprises 784 input features,
which are the pixels of the input images (dimension
28 ×28) and 128 output features.
(b).Spiking Activation Layer: It generates a certain
number of spikes per simulated second corresponding
to the prediction of the input features by the Spik-
ingReLU activation function. SpikingReLU is chosen
because it is the best fit for a Spiking Activation
function, unlike sigmoid or glorot functions. This
layer adds a temporal dimension to our model. This 
is where the energy efficiency of SNNs becomes
important; if the spikes are generated very rapidly,
then the prediction might not be propagated to the
further layer and if the spikes are fired for long, then it
would be a waste of energy.
( c ) Temporal Average Pooling layer: This layer
takes the time average of the spikes generated by the
preceding layer and propagates this to the Dressed
Quantum Net.
2. [5-ary]_pretrain_6x2_squeeze.ipynb
It is used to train the proposed DSQ-Net model
for the 5-class image datasets. The classical pre-
trained model is loaded from the .h5 file in the
variable called spikeaware_model and then the
class DressedQuantumNet defined. This class
defines a layer to wrap a variational quantum
layer with a pre and a post network, both classi-
cal and Linear. Before adding this layer to out
pre-trained model, we removed the last layer of
the model loaded in variable spikeaware_model
by the following line of code: model_hybrid =
copy.deepcopy(torch.nn.Sequential(∗(list
(spikeaware_model.children())[: −1])))
Next, the trainable parameters are frozen
by using the snippet: for parameter in
model_hybrid.parameters() :
param.requires_grad = False and the final classi-
fication layer is added by the following line of code:
model_hybrid.fc = DressedQuantumNet() the
labels are modified by : train_labels− = 6 to make
them compatible with the modified structure.
3. [5-ary]_pretrain_6x2_squeeze_KMNIST.ipynb
It contains the codes to train the hybrid classical-
quantum networks (6 qubits ansatz) with the given
KMNIST dataset. It works in the same way as the
[5-ary]_pretrain_6x2_squeeze.ipynb
notebook, but for KMNIST dataset.
4. [5-ary]_pretrain_6x2_squeeze_MNIST.ipynb
It comprises the codes to train the hybrid classical-
quantum network (6 qubits ansatz) with MNIST
dataset. It works in the same way as the
[5-ary]_pretrain_6x2_squeeze.ipynb
notebook, but for the MNIST dataset.
5. [5-ary]_pretrain_6x2_squeeze_INET.ipynb
It comprises the codes to train the hybrid classical-
quantum network (6 qubits ansatz) with MNIST
dataset. It works in the same way as the
[5-ary]_pretrain_6x2_squeeze.ipynb
notebook, but for the ImageNet dataset.
6. [5-ary]_pretrain_6x2_squeeze_CIFAR.ipynb
It comprises the codes to train the hybrid classical-
quantum network (6 qubits ansatz) with MNIST
dataset. It works in the same way as the
[5-ary]_pretrain_6x2_squeeze.ipynb
notebook, but for the CIFAR dataset.
7. data_create_FASHIONMNIST.ipynb
It comprises codes to create noisy version of Fashion-
MNIST dataset. It converts the 7200 test images to
their noise affected versions. Various types of noises
are added in various intensities and are arranged in an
order compatible with the proposed DSQ-Net model.
8. data_create_KMNIST.ipynb
It contains codes to create noisy version of KMNIST
dataset. Its function is similar to the jupyter notebook
named data_create_FASHIONMNIST.ipynb.
9. data_create_MNIST.ipynb
It comprises codes to create noisy version of MNIST
dataset.Its function is similar to the jupyter notebook
named data_create_FASHIONMNIST.ipynb.
10. data_create_INET.ipynb
It comprises codes to create noisy version of ImageNet
dataset.Its function is similar to the jupyter notebook
named data_create_FASHIONMNIST.ipynb.
11. data_create_CIFAR.ipynb
It comprises codes to create noisy version of CIFAR
dataset.Its function is similar to the jupyter notebook
named data_create_FASHIONMNIST.ipynb.
12. Testbench_Fashion_5_class.ipynb
It contains the codes for testing networks against noisy
version of 5-class Fashion MNIST dataset. It is an or-
ganised form of dealing with the test data and useful
for plotting and other datapoints.
13. Testbench_KMNIST_5_class.ipynb
It includes the codes for testing networks on noisy ver-
sion of 5-class KMNIST dataset.
14. Testbench_MNIST_5_class.ipynb
This section of the codes is used for testing networks
on noisy version of 5-class MNIST dataset.
15. Testbench_INET_5_class.ipynb
This section of the codes is used for testing networks
on noisy version of 5-class ImageNet dataset.
16. Testbench_CIFAR_5_class.ipynb
This section of the codes is used for testing networks
on noisy version of 5-class CIFAR dataset.



