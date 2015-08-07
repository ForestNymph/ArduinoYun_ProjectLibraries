/*
 * MQ2.h
 *
 *  Created on: Aug 7, 2015
 *      Author: Sylwia Grudowska
 */

/*******************Demo for MQ-2 Gas Sensor Module V1.0*****************************
 Support:  Tiequan Shao: support[at]sandboxelectronics.com

 Licence: Attribution-NonCommercial-ShareAlike 3.0 Unported (CC BY-NC-SA 3.0)

 Note:    This piece of source code is supposed to be used as a demostration ONLY. More
 sophisticated calibration is required for industrial field application.

 Sandbox Electronics    2011-04-25
 ************************************************************************************/

#ifndef MQ2_h
#define MQ2_h

/************************Hardware Related Macros************************************/

#define         RL_VALUE                     (5)     //define the load resistance on the board, in kilo ohms
#define         RO_CLEAN_AIR_FACTOR          (9.83)  //RO_CLEAR_AIR_FACTOR=(Sensor resistance in clean air)/RO,
//which is derived from the chart in datasheet

/***********************Software Related Macros************************************/
#define         CALIBARAION_SAMPLE_TIMES     (50)    //define how many samples you are going to take in the calibration phase
#define         CALIBRATION_SAMPLE_INTERVAL  (500)   //define the time interal(in milisecond) between each samples in the
//cablibration phase
#define         READ_SAMPLE_INTERVAL         (50)    //define how many samples you are going to take in normal operation
#define         READ_SAMPLE_TIMES            (5)     //define the time interal(in milisecond) between each samples in
//normal operation

/**********************Application Related Macros**********************************/
#define         GAS_LPG                      (0)
#define         GAS_CO                       (1)
#define         GAS_SMOKE                    (2)

/*****************************Globals***********************************************/

class MQ2 {

public:

	/*****************************  MQGetGasPercentage **********************************
	 Input:   rs_ro_ratio - Rs divided by Ro
	 gas_id      - target gas type
	 Output:  ppm of the target gas
	 Remarks: This function passes different curves to the MQGetPercentage function which
	 calculates the ppm (parts per million) of the target gas.
	 ************************************************************************************/
	int MQGetGasPercentage(float rs_ro_ratio, int gas_id);

	/****************** MQResistanceCalculation ****************************************
	 Input:   raw_adc - raw value read from adc, which represents the voltage
	 Output:  the calculated sensor resistance
	 Remarks: The sensor and the load resistor forms a voltage divider. Given the voltage
	 across the load resistor and its resistance, the resistance of the sensor
	 could be derived.
	 ************************************************************************************/
	float MQResistanceCalculation(int raw_adc);

	//with these two points, a line is formed which is "approximately equivalent"
	//to the original curve.
	//data format:{ x, y, slope}; point1: (lg200, 0.53), point2: (lg10000,  -0.22)
	float Ro = 10; //Ro is initialized to 10 kilo ohms

private:
	float LPGCurve[3] = { 2.3, 0.21, -0.47 }; //two points are taken from the curve.
	//with these two points, a line is formed which is "approximately equivalent"
	//to the original curve.
	//data format:{ x, y, slope}; point1: (lg200, 0.21), point2: (lg10000, -0.59)
	float COCurve[3] = { 2.3, 0.72, -0.34 }; //two points are taken from the curve.
	//with these two points, a line is formed which is "approximately equivalent"
	//to the original curve.
	//data format:{ x, y, slope}; point1: (lg200, 0.72), point2: (lg10000,  0.15)
	float SmokeCurve[3] = { 2.3, 0.53, -0.44 }; //two points are taken from the curve.

	/*****************************  MQGetPercentage **********************************
	 Input:   rs_ro_ratio - Rs divided by Ro
	 pcurve      - pointer to the curve of the target gas
	 Output:  ppm of the target gas
	 Remarks: By using the slope and a point of the line. The x(logarithmic value of ppm)
	 of the line could be derived if y(rs_ro_ratio) is provided. As it is a
	 logarithmic coordinate, power of 10 is used to convert the result to non-logarithmic
	 value.
	 ************************************************************************************/
	int MQGetPercentage(float rs_ro_ratio, float *pcurve);

};
#endif
//
// END OF FILE
//



