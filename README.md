# == BMsim challenge ==
Welcome to the repository of the Bloch-McConnell simulation (BMsim) challenge. 
The idea of the challenge can be summarized as follows:

  1) Every participant simulates 3 different well-defined cases / scenarios
  2) The simulation results from all participants are collected
  3) The median Z-spectrum wins

In this first challenge, we have chosen 3 different preparation schemes consisting of single block pulses / CW pulses only. Next challenges might cover more sophisticated cases using arbitrary shaped RF pulses as well.

## Simulation results
To keep the burden for posting your simulation results as low as possible, we decided to collect the results in a simple
Google Docs spreadsheet that can be found here:

https://docs.google.com/spreadsheets/d/1JN7VN-f1ktDrJgokb0FlUFwkH0MWYlPA_jSfnQoFOVc/

Please feel free to add your name / group in case it's not listed yet and post your results.

## Online evaluation script
To provide a simple way to compare your own simulation results with (a selection of) the results collected in the [google spreadsheet](https://docs.google.com/spreadsheets/d/1JN7VN-f1ktDrJgokb0FlUFwkH0MWYlPA_jSfnQoFOVc/), we set up an [online evaluation script](https://colab.research.google.com/drive/1csiIjK-fiftdb7OwvJ84gWuv8lLADgv7) in form of a iPython Notebook that is hosted on Google colab. 

## Simulation cases
### General settings / assumptions:
  1) fully relaxed initial magnetization (Zi = 1) for every offset,this is equivalent to a very long recovery time 10*T1	
  2) post-preparation delay = 6.5 ms, in the pulseq-file this corresponds to the gradient spoiler duration
  3) gyromagnetic ratio: 42.5764 MHz/T
  4) larmor frequency (3T): 127.7292 MHz/T  
  5) Normalization scan at -300 ppm
  
### Case 1: 2 pool model, APTw preparation - steady-state
  - **pool model**: 2 pool model of creatine as defined in [case_1_2pool_model.yaml](/case_1/case_1_2pool_model.yaml)
  - **prep. details**:
    - pulse shape: block
    - pulse duration: 15 s
    - pulse power: 2 µT
    - offset list: -15:0.1:15 ppm

More details about the pool model and preparation scheme can be found in the corresponding [README](/case_1/README.md)

### Case 2: 2 pool model, APTw preparation
  - **pool model**: 2 pool model of creatine as defined in [case_2_2pool_model.yaml](/case_2/case_2_2pool_model.yaml)
  - **prep. details**:
    - pulse shape: block
    - pulse duration: 2 s
    - pulse power: 2 µT
    - offset list: -15:0.1:15 ppm

More details about the pool model and preparation scheme can be found in the corresponding [README](/case_2/README.md)

### Case 3: 5 pool model, APTw preparation
  - **pool model**: 5 pool model of WM as defined in [case_3_5pool_model.yaml](/case_3/case_3_5pool_model.yaml)
  - **prep. details**:
    - pulse shape: block
    - pulse duration: 2 s
    - pulse power: 2 µT
    - offset list: -15:0.1:15 ppm

More details about the pool model and preparation scheme can be found in the corresponding [README](/case_3/README.md)

### Case 4: 5 pool model, WASABI preparation
  - **pool model**: 5 pool model of WM as defined in [case_4_5pool_model.yaml](/case_4/case_4_5pool_model.yaml)
  - **prep. details**:
    - pulse shape: block
    - pulse duration: 5 ms
    - pulse power: 3.7 µT
    - offset list: -2:0.05:2 ppm

More details about the pool model and preparation scheme can be found in the corresponding [README](/case_4/README.md)

## FAQ
#### How did you choose the value of the gyromagnetic ratio?

The [NIST value of the shielded proton gyromagnetic ratio](https://physics.nist.gov/cgi-bin/cuu/Value?gammapp) is
2.675153151 x 10<sup>8</sup> s<sup>-1</sup> T<sup>-1</sup>. Dividing this value by 2 Pi yields 42.576384750950949004433240733872 MHz/T, which results
in the used value of 42.5764 MHz/T when rounded to 4 digits.

Please make sure to use these values for gamma in your simulations:
  - 42.5764 MHz/T
  - 42.5764 x 2 x Pi s<sup>-1</sup> T<sup>-1</sup> (do **NOT** use the exact NIST value)


#### How do you define the pool size fraction f?
There could be different definitions of the fraction, some define water f=1, and all other relative to water.
Others define M0i of each pool i and then normalize fi= M0i/sum_i(M0i)

This could lead to differences, but we decided NOT to dictate which definition to use.

#### How do you define the MT pool?
Some simulations use x, y, and z components to describe a Lorentzian MT pool.
Others use only the z-component and assume a Lorentzian lineshape factor there.
Again, we decided NOT to dictate how to simulate the MT.
