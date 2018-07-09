# Estimation Project #

## The Tasks ##

 - [Step 1: Sensor Noise](#step-1-sensor-noise)
 - [Step 2: Attitude Estimation](#step-2-attitude-estimation)
 - [Step 3: Prediction Step](#step-3-prediction-step)
 - [Step 4: Magnetometer Update](#step-4-magnetometer-update)
 - [Step 5: Closed Loop + GPS Update](#step-5-closed-loop--gps-update)
 - [Step 6: Adding Your Controller](#step-6-adding-your-controller)

### Step 1: Sensor Noise ###

The standard deviation of sensors are computed with a python script, simply by reading in all data
into a list and applying `std()` function in numpy. GPS standard deviation is 0.7053.
Accelerometer standard deviation is 0.4895.

### Step 2: Attitude Estimation ###

Implemented in `UpdateFromIMU()`. Roll, pitch, yaw information is converted from global frame into
body frame. These values are integrated with measurements from gyro sensors. Roll, pitch, yaw values
after integration are converted back to global frame.

![attitude_estimation](images/sim_attitude_estimation.png)

### Step 3: Prediction Step ###

Implemented in `Predict()`.
New state is computed by `PredictState()` function.
The covariance is computed from `Σt = GtΣt−1GTt + Qt`, where `Gt` is the `gPrime` matrix.
Part of `gPrime` matrix is computed by `GetRbgPrime()`.

![predict_formula](images/formula_predict.png)

![predict_state](images/sim_predict_state.png)

![predict_cov](images/sim_predict_cov.png)

### Step 4: Magnetometer Update ###

Implemented in `UpdateFromMag()`. Yaw state is updated with information from magnetometer.
`hPrime` only has last entry as 1 since only yaw will be updated.

![mag_update_formula](images/formula_mag_update.png)

![mag_update](images/sim_mag_update.png)

### Step 5: Closed Loop + GPS Update ###

Implemented in `UpdateFromGPS()`. State variables are updated with matrix `hPrime`.

![gps_update_formula](images/formula_gps_update.png)

![gps_update](images/sim_gps_update.png)

### Step 6: Adding Your Controller

Controller is de-tuned to stablize scenario `11_GPSUpdate`.
