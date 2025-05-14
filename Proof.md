## Simulator Descriptions

### - **Corrupted sender S**

For the simulator Sim_S, the simulated view for the corrupt sender S is constructed as follows:

Given the input set X, Sim_S randomly selects a public key pk' to replace the receiver's original public key pk, and randomly samples a set of hash functions {H_h^{1'}, H_h^{2'}} for h in [3] to substitute the agreed-upon hash functions.
Using pk' and {H_h^{1'}, H_h^{2'}}, Sim_S constructs a simulated DPC' structure with dummy elements replaced by random values, and encrypts it using the underlying FHE scheme.
Due to the IND-CPA security of the FHE scheme and the fact that hash functions behave like random oracles with overwhelming probability, the simulated DPC' is computationally indistinguishable from the real DPC.
Moreover, since Sim_S does not receive any message during the protocol, the simulated view is indistinguishable from the real view.


### - **Corrupted cloud server C**

For the simulator Sim_C, the simulated view for the corrupt cloud server C is constructed as follows:

The encrypted DPC and VPC are provided by the sender S and the receiver R, respectively. Since Sim_C has no knowledge of the FHE scheme’s secret key sk, the public key pk, or the hash functions used in constructing the DPC and VPC, it cannot decrypt any ciphertexts.
Furthermore, the ciphertexts and index information in both the DPC and VPC appear indistinguishable from random values to Sim_C. Therefore, the corrupted cloud server C cannot distinguish between the real-world view and the simulated view.


### - **Corrupted receiver R**

For the simulator Sim_R, the simulated view for the corrupt receiver R is constructed as follows:

Given the input set Y, similar to the simulator Sim_S, Sim_R randomly selects a fresh key pair (pk', sk') to replace the original FHE key pair (pk, sk), and chooses a fresh set of random hash functions {H_h^{1'}, H_h^{2'}} for h in [3] to replace the originally agreed-upon hash functions.
In the offline setup phase, Sim_R constructs a simulated virtual permuted cuckoo hash table VPC', where each virtual element is replaced with a random value.
Due to the semantic security of the underlying FHE scheme and the randomness of the selected hash functions, the simulated VPC' is computationally indistinguishable from a real VPC.
During the online computation phase, Sim_R receives the homomorphic computation result Ans from the cloud server.
Since Ans appears random before decryption and provides no meaningful information after decryption (with respect to the sender’s input), the corrupted receiver R learns nothing about the sender’s set. Therefore, the simulated view is computationally indistinguishable from the real-world view.
