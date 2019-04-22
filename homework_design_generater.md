# WAVE GENERATER - HOMEWORK



### Main
* init: watch dog, osc, timer, led, generater
* the WHILE loop scans keyboard input array. The mode changing, frequency setting and amplify setting are processed here.





### Timer 0
Timer0 circularly refreshs the LED digital to display numbers, the numbers displayed only depend on the following array.  
####API

* LED_BUF[0-5]



### Timer 1
Timer1 is used as a circularly generater, the numbers in the sin_seq_out can be modified in some other parts thus they can be used to control the amplify rate. The frequency is controled by the th and tl.   
####API  
	sin_seq_out[0-frames_per_term]  
	th_1,tl_1

### NUMBERS
#### Global Parameters
	int frames_per_term = 160 // 
	float time_for_per_count = 0.1 // 
	float ratio_DAC_to_votage = 0.1 // 

#### Global Variables

	frames_per_term; // 
	sin[frames_per_term]; // this is a buffer of a sin sequence, will been deleted soon
	am_seq_raw[frames_per_term]; // this is a buffer for the am sequence, will be deleted soon
	char am_mode = 0; // control the mode
	int count_to_overflow;
	unsigned char tl0,th0,tl1,th1; // 0 is for led , and 1 is for wave generater


#### Pre-defined Data
	unsigned char LINE[4];
	unsigned char DIGI[16];
	unsigned char KEY[4];
	unsigned char am_seq_raw[frames_per_term];
	static unsigned char LED_BUF[6]={0xff,0xff,0xff,0xff,0xff,0xff};


### Frequency and Amplify Setting
	void set_freq_amp(unsigned int freq,unsigned char amp){
	int count_to_overflow; // tempororily used in the frequency caculating part    
	am_mode = 0;
	// caculate the output sequence
	for(i=0;i<frames_per_term;i++){
		sin_seq_out[i] = (int)(math.sin(2*math.pi*(i/frames_per_term))*voltage*ratio_DAC_to_votage) // DAC can only be input with int, and char is acceptble
	}
	// caculate the overflow time
	count_to_overflow = int((1/(freq*frames_per_term))/(time_for_per_count))
	th1 = count_to_overflow / 256
	tl1 = count_to_overflow % 256

}


