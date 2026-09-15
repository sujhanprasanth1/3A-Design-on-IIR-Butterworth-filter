# IIR-FILTER-DESIGN
# EXP 3 A: DESIGN OF LOW PASS BUTTERWORTH FILTER USING BILINEAR TRANSFORMATION TECHNIQUE

# AIM: 

# To perform design of Butterworth Filter Using Impulse Invariant and Bilinear Transformation Techniques using SCILAB.

# APPARATUS REQUIRED: 
PC installed with SCILAB. 

# PROGRAM: 

## Impulse Invariant Method
clc; 
clear; 
close; 
// Input specifications 
wp = input('Enter the pass band frequency (Radians)= '); 
ws = input('Enter the stop band frequency (Radians)= '); 
alphap = input('Enter the pass band attenuation (dB)= '); 
alphas = input('Enter the stop band attenuation (dB)= '); 
T = input('Enter the sampling time = '); 
// Convert digital frequencies to analog frequencies
omegap = wp/T; 
disp(omegap,'omegap='); 
omegas = ws/T; 
disp(omegas,'omegas=');
 // Calculate filter order 
N = log10(((10^(0.1*alphas))-1)/((10^(0.1*alphap))-1))/(2*log10(omegas/omegap)); 
disp(N,'N='); 
N = ceil(N); 
disp(N,'Rounded value of N='); 
// Cutoff frequency 
omegac = omegap/((10^(0.1*alphap)-1)^(1/(2*N))); 
disp(omegac,'omegac=');
 // Normalized Analog LPF 
disp('Normalized Analog LPF Transfer Function H(s)'); 
Hs_normal = analpf(N,'butt',[0,0],1); 
disp(Hs_normal); 
// Analog Butterworth LPF
 disp('Analog LPF Transfer Function H(s)'); 
Hs = analpf(N,'butt',[0,0],omegac); 
disp(Hs); 
// Impulse Invariant Transformation 
Hz = dscr(Hs,T); 
disp('Digital LPF Transfer Function H(z)'); 
disp(Hz);
 // Frequency response 
HW = frmag(Hz,512);
 w = 0:%pi/511:%pi; 
plot(w/%pi,abs(HW)); 
xlabel('Normalized Digital Frequency'); 
ylabel('Magnitude');
 title('Frequency Response of Butterworth IIR LPF using Impulse Invariant Method');

 ## Bilinear Transformation Method
clc ;
close ;
wp=input('Enter the pass band frequency (Radians )= ' );
ws=input('Enter the stop band frequency (Radians )= ' );
alphap=input( ' Enter the pass band attenuation (dB)=' );
alphas=input( ' Enter the stop band attenuation(dB)=' );
T=input('Enter the Value of sampling Time=');
//Pre warping- Bilinear Transformation
omegap=(2/T)*tan(wp/2);
disp(omegap,'omegap=');
omegas=(2/T)*tan(ws/2);
disp(omegas,'omegas=');
//Order of the filter
N=log10(((10^(0.1*alphas))-1)/((10^(0.1*alphap))-1))/(2*log10(omegas/omegap));
disp(N,'N=');
N=ceil(N);
disp(N,'Round off value of N=');
//Cut off frequency
omegac=omegap/(((10^(0.1*alphap)) -1)^(1/(2* N)));
disp(omegac,'omegac=');
disp('Normalised Analog LPF Transfer function H(S)=');
hs_Normalised = analpf(N,'butt',[0,0],1);
disp(hs_Normalised);
disp('Analog LPF Transfer function H(S)=');
hs= analpf(N,'butt',[0,0],omegac);
disp(hs);
z=poly(0,'z');//Defining variable z
Hz=horner(hs,(2/ T)*((z -1)/(z+1)))// Bilinear Transformation
disp('Digital LPF Transfer function H(Z)=');
disp(Hz);
HW=frmag(Hz,512); // Frequency response
w=0:%pi/511:%pi ;
plot(w/%pi,abs(HW));
xlabel(' Normalized Digital Frequency w');
ylabel('Magnitude ');
title(' Frequency Response of Butterworth IIR LPF');


# OUTPUT: 
<img width="1317" height="689" alt="image" src="https://github.com/user-attachments/assets/d4265cf2-e63f-453b-acf6-dda287fbef64" />
<img width="931" height="726" alt="image" src="https://github.com/user-attachments/assets/5accd96a-e950-46de-8cee-17b8cb11b17c" />



# RESULT: 

Thus, design of Butterworth Low pass IIR filter waveforms were plotted and output was verified.

