# Numpy_Neural_Library

This is the code for a neural network library. It is similar to tensorflow, but it easy to add your own layers. 
To use this, you will have to download all the code, create a new file for you network, then build the network there.
The syntax for this library is relative easy to learn, and it is somewhat simple. The explaination for the functions are below.
This code runs on Python 3.5+, and requires the Numpy package. If this gets a good response, I will try and make it a package on PyPi.

The functions are explained here:

To create a new neural network, you will first have to import all required functions. The file name is always lower case, and the words are separated by an underscore.
The function is the same as the file name, but in pascal case. To start off, the first function to import is the network function. It can be imported by typing:
  
    from network import Network
    net = Network()
  
You can the add layers to the network. There are a few different layer types to be imported:
  1) fc_layer
  2) conv_layer
  3) activation_layer

They can be added by typing:

      from network import Network
      from fc_layer import FCLayer
      from activation_layer import ActivationLayer
      from activations import tanh, tanh_prime
      
      net = Network()
      net.add(FCLayer(2,3))
      net.add(ActivationLayer(tanh, tanh_prime))
      net.add(FCLayer(3,1))
      net.add(ActivationLayer(tanh, tanh_prime))
      
When making a neural network, you have to have an actiavtion layer after each layer. Otherwise, there will be no activations in the network. The program comes with a few different activations, which you can see in the activations.py file.

Now that the network is built, you can then train it. There is a function in the network.Network class, which trains it. But, before you do that, you have to include the lose functions, and the code includes one loss function: mse, and it's prime: mse_prime. They can be inputted into the network with the following code:

    from network import Network
    from fc_layer import FCLayer
    from activtion_layer import ActivationLayer
    from activations import tanh, tanh_prime
    from losses import mse, mse_prime
    
    x_train = np.array([[[0,0], [0,1], [1,0], [1,1]]])
    y_train = np.array([[[0], [1], [1], [0]]])
    
    net = Network()
    net.add(FCLayer(2,3))
    net.add(ActivationLayer(tanh, tanh_prime))
    net.add(FCLayer(3,1))
    net.add(ActivationLayer(tanh, tanh_prime))
    
    net.use(mse, mse_prime)
    net.fit(x_train, y_train, epochs=1000. learning_rate=0.1)
    
For this example, the x_train, and y_train is for a xor dataset. The full code is in the file example_xor.py. The neural network is also tailored for this dataset.

Once you have trained the network, you can the make predications. That can be done with this code. This is the full example:

    from network import Network
    from fc_layer import FCLayer
    from activation_layer import ActivationLayer
    from activations import tanh, tanh_prime
    from losses import mse, mse_prime
    
    x_train = np.array([[[0,0], [0,1], [1,0], [1,1]]])
    y_train = np.array([[[0], [1], [1], [0]]])
    
    net = Network()
    net.add(FCLayer(2,3))
    net.add(ActivationLayer(tanh, tanh_prime))
    net.add(FCLayer(3,1))
    net.add(ActivationLayer(tanh, tanh_prime))
    
    net.use(mse, mse_prime)
    net.fit(x_train, y_train, epochs=1000, learning_rate=0.1)
    
    out = net.predict(x_train)
    
    print('Expected:', y_train)
    print('Predicted:', out)
    
That should output both the correct values, and the outputed values, from the network.
