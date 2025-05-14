## Simulator Description for Corrupted Parties

- **Corrupted sender \(S\)**:  
  For the simulator \(\mathsf{Sim}_S\), the simulated view for the corrupted sender \(S\) is constructed as follows:  
  Given the input set \(X\), \(\mathsf{Sim}_S\) randomly selects a public key \(pk'\) to replace the receiver’s original public key \(pk\), and randomly samples a set of hash functions \(\{H_h^{1'}, H_h^{2'}\}_{h \in [3]}\) to replace the originally agreed-upon hash functions.  
  Using \(pk'\) and \(\{H_h^{1'}, H_h^{2'}\}\), \(\mathsf{Sim}_S\) constructs a simulated \(DPC'\) structure where dummy elements are replaced by random values, and encrypts them using the underlying FHE scheme.  
  Due to the IND-CPA security of the FHE scheme and the fact that the hash functions behave like random oracles with overwhelming probability, the simulated \(DPC'\) is computationally indistinguishable from the real DPC.  
  Moreover, since \(\mathsf{Sim}_S\) does not receive any messages during the protocol, the simulated view is indistinguishable from the real view.

- **Corrupted cloud server \(C\)**:  
  For the simulator \(\mathsf{Sim}_C\), the simulated view for the corrupted cloud server \(C\) is constructed as follows:  
  The encrypted DPC and VPC are provided by the sender \(S\) and receiver \(R\), respectively.  
  Since \(\mathsf{Sim}_C\) has no knowledge of the FHE scheme’s secret key \(sk\), the public key \(pk\), or the hash functions used to construct the DPC and VPC, it cannot decrypt any ciphertexts.  
  Furthermore, the ciphertexts and index information in both DPC and VPC appear indistinguishable from random values to \(\mathsf{Sim}_C\).  
  Therefore, the corrupted cloud server \(C\) cannot distinguish between the real-world view and the simulated view.

- **Corrupted receiver \(R\)**:  
  For the simulator \(\mathsf{Sim}_R\), the simulated view for the corrupted receiver \(R\) is constructed as follows:  
  Given the input set \(Y\), similar to \(\mathsf{Sim}_S\), the simulator \(\mathsf{Sim}_R\) randomly selects a fresh key pair \((pk', sk')\) to replace the original FHE key pair \((pk, sk)\), and selects a new set of random hash functions \(\{H_h^{1'}, H_h^{2'}\}_{h \in [3]}\) to replace the originally agreed-upon hash functions.  
  In the offline setup phase, \(\mathsf{Sim}_R\) constructs a simulated virtual permuted cuckoo hash table \(VPC'\), where each virtual element is replaced with a random value.  
  Due to the semantic security of the underlying FHE scheme and the randomness of the selected hash functions, the simulated \(VPC'\) is computationally indistinguishable from the real \(VPC\).  
  During the online computation phase, \(\mathsf{Sim}_R\) receives the homomorphic computation result \(Ans\) from the cloud server.  
  Since \(Ans\) appears random before decryption and reveals no meaningful information after decryption (with respect to the sender’s input), the corrupted receiver \(R\) learns nothing about the sender’s set.  
  Therefore, the simulated view is computationally indistinguishable from the real-world view.
