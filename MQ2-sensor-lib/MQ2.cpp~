/*
 * MQ2.cpp
 *
 *  Created on: Aug 7, 2015
 *      Author: Sylwia Grudowska
 */

#include "MQ2.h"
#include <math.h>



int MQ2::MQGetGasPercentage(float rs_ro_ratio, int gas_id) {
	if (gas_id == GAS_LPG) {
		return MQGetPercentage(rs_ro_ratio, LPGCurve);
	} else if (gas_id == GAS_CO) {
		return MQGetPercentage(rs_ro_ratio, COCurve);
	} else if (gas_id == GAS_SMOKE) {
		return MQGetPercentage(rs_ro_ratio, SmokeCurve);
	}

	return 0;
}

int MQ2::MQGetPercentage(float rs_ro_ratio, float *pcurve) {
	return (pow(10, (((log(rs_ro_ratio) - pcurve[1]) / pcurve[2]) + pcurve[0])));
}

float MQ2::MQResistanceCalculation(int raw_adc) {
	return (((float) RL_VALUE * (1023 - raw_adc) / raw_adc));
}


