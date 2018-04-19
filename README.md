# Lstm-Variational-Auto-encoder

#  ![CI status](https://img.shields.io/cocoapods/l/AFNetworking.svg)

Variationnal auto-encoder for anomaly detection/features extraction, with lstm cells (stateless or statefull). 

## Installation

### Requirements


`$ pip install --upgrade git+https://github.com/Danyleb/Lstm-Variational-Auto-encoder.git`

## Usage

```python
from LstmVAE import LSTM_Var_Autoencoder
from LstmVAE import preprocess

df = preprocess(input) #return standardized and normalized df, check NaN values replacing it with 0

df = df.reshape(-1,timesteps,n_dim) #use 3D input, n_dim = 1 for 1D time series. 

vae = LSTM_Var_Autoencoder(intermediate_dim = 15,z_dim = 3, n_dim=1, stateful = True) #default stateful = False

vae.fit(df, learning_rate=0.001, batch_size = 100, num_epochs = 200, opt = tf.train.AdamOptimizer, REG_LAMBDA = 0.01,
            grad_clip_norm=10, optimizer_params=None, verbose = True)

"""REG_LAMBDA is the L2 loss lambda coefficient, should be set to 0 if not desired.
   optimizer_param : pass a dict = {}
"""

x_reconstructed, recons_error = vae.reconstruct(df, get_error = True) #returns squared error

x_reduced = vae.reduce(df) #latent space representation
```



## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.


## License
[MIT](https://choosealicense.com/licenses/mit/)
