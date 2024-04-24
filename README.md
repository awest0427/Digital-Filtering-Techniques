# Digital Filtering Techniques
A software defined radio(SDR) implements the functions of traditional radio hardware components (such as mixers, filters, and amplifiers) using software on a computer. In software defined radios, digital filtering techniques can be used for signal processing.

The MATLAB code allows users design and analyze a variety of filters that would be applied to complex-baseband data to display the complex filtering. The following 4 standard filter types will be designed: lowpass, highpass, bandpass, and bandstop. 

The main tool used is the Filter Design and Analysis tool, which allows you to design and analyze multiple filters. Using the Filter Design and Analysis tool(fdatool), in MATLAB, each filter type was designed with a design method and different specifications were set. Random noise was generated to show a real signal representation and got added to the complexd baseband signal. The waveform generator can be used to capture the signals before and after the noise is applied to be able to do a comparision. 

Sample of code for Bandpass filter
```matlab
%% Generating QAM waveform
% QAM configuration
M = 4; 	 % Modulation order
% input bit source:
in = randi([0, 1], 60000, 1);

% Generation
waveform0 = qammod(in, M, 'gray', 'InputType', 'bit', 'UnitAveragePower', true);

Fs = 1000; 								 % Specify the sample rate of the waveform in Hz

%% Impairments
% AWGN
waveform = awgn(waveform0, 20, 'measured');

%% Visualize
% Time Scope
timeScope = timescope('SampleRate', Fs, ...
    'TimeSpanOverrunAction', 'scroll', ...
    'TimeSpanSource', 'property', ...
    'TimeSpan', 0.03);
timeScope(waveform);
release(timeScope);

dur = 29.9990;
t = 0:1/Fs:dur;

% Constellation Diagram
constel = comm.ConstellationDiagram('ColorFading', true, ...
    'ShowTrajectory', 0, ...
    'ShowReferenceConstellation', false);
constel(waveform);
release(constel);

load('BandPassF.mat');
% Apply filter
filtered_signal = filter(Bandp, waveform);

% Create 1st spectrumAnalyzer display - Original wavform
sa0 = spectrumAnalyzer;
spectrum0 = spectrumAnalyzer('SampleRate', Fs);
spectrum0(waveform0);
release(spectrum0);

% Create 2nd spectrumAnalyzer display - Noisy wavform
sa1 = spectrumAnalyzer;
spectrum1 = spectrumAnalyzer('SampleRate', Fs);
spectrum1(waveform);
release(spectrum1);

% Create 3rd spectrumAnalyzer display - filtered wavform
sa2 = spectrumAnalyzer;
spectrum2 = spectrumAnalyzer('SampleRate', Fs);
spectrum2(filtered_signal);
release(spectrum2);

figure(1);
subplot(2,1,1);
plot(t(1:301), waveform(1:301), 'b', t(1:301), waveform0(1:301), 'r');
title('Noisy vs Original');
xlabel('Time (s)');
ylabel('Amplitude');
legend('Noisy Signal', 'Original');
ylim([-1.5,1.5]);

figure(1);
subplot(2,1,2);
plot(t(1:301), waveform(1:301), 'b', t(1:301), filtered_signal(1:301), 'r');
title('Noisy vs Filtered Signal');
xlabel('Time (s)');
ylabel('Amplitude');
legend('Noisy Signal', 'Filtered Signal');
ylim([-1.5,1.5]);
```
Example of Low Pass Filter using the Filter Design and Analysis Tool
![image](https://github.com/awest0427/Digital-Filtering-Techniques/assets/167692889/476be309-c7df-4b2f-9fa4-50ce0424401e)

The Digital Filtering pdf helps walk through the designing of the different filters and how to incorporate it into the MATLAB code.



