# ustHRV
Validation of the ultra-short-term heart rate variability (ustHRV) measures under changing psychophysiological state of the healthy participants at rest

This project investigates which statistical and spectral HRV measures may be reliably assessed from shorter ECG lengths compared to the benchmark 5-min recording. In addition, we investigated how changes in the psychophysiological state of the participants due to mental fatigue and drowsiness and the difference in the sensory processing impact the agreement of ustHRV surrogates with the reference signal. The correlation analysis, intra- and inter-group statistical tests, trend analysis, and Bland-Altman plots showed that the statistical measures and HF power from the recordings of as short as 30 s and the other frequency measures of 1 min are good surrogates of the stHRV when the participants are rested and vigilant. Longer recordings may be needed with increasing mental fatigue or drowsiness. This work lays the path to the novel applications of the ustHRV analysis in dynamic environments and factors changing human’s psychophysiological state.

ECG pre-processing was done using Acqknowledge 4.2 software (Biopac Systems Inc., USA), and HRV analysis was done using AcqKnowledge 5.0 software (Biopac Systems Inc., USA).

ECG pre-processing

Before starting processing the data, please make sure you know what the normal ECG signal looks like. You can use the sample data files provided by Biopac in the first window that opens after executing the program: ‘ECG_LeadII’.
1.	Load the ECG file: File -> Open
2.	If the ECG signal is longer than 5 min -> trim it at the beginning and end so that precisely 5 min of recording is left (no cycle was cut in between): Edit -> Cut
3.	Quality check 1: Check if the baseline (time after the end of T wave and before the P wave of the next cycle) is around 0 mV
4.	If quality check 1 not fulfilled -> scale the waveform to move the baseline around 0 ms: First calculate the mean baseline in the waveform: choose I-beam cursor -> find the baseline fragment in the signal -> mark the fragment of the signal within the baseline period -> in the quick measurement menu choose ‘Mean’ and read the value. You can do it for a few cycles and extract the average -> use this value to correct for the shift from the baseline ->
Transform -> Waveform math -> In ‘source 1’ box: ECG channel, ‘+’, ‘K’, => the same channel; K = the value calculated before with the shift of the baseline -> check if the baseline was corrected.
5.  Do a quick visual inspection to check if there are any abnormalities in the signal.
6.  Plot the heart rate (HR) channel: Analysis -> Find rate -> Ok -> look at the Rate channel -> check if the waveform is within a relatively narrow band: HR should be within physiological range (~60-90 BPM), no high amplitude spikes
7.  If there is an artifact -> remove the artifact using ‘connect endpoints’ option: using I-beam cursor mark the fragment of the signal that contains the artifact (a little before the beginning of the artifact and after the end of the artifact) -> Transform -> Math functions -> Connect Endpoints. IMPORTANT: you cannot remove QRS complex, as it will distort the HRV analysis. This applies only to fragments of the signal without QRS complex!!!
8.  Locate ECG parameters: Analysis -> Locate complex boundaries
9.  Do a quality check: visually scan the entire signal and make sure all the ECG labels are in the right place in all the ECG cycles

HRV analysis
1. First, plot only the tachogram (values of the RR intervals plotted against the number of beats): Analysis -> Heart Rate Variability -> Change method to locate the QRS complexes to ‘Events’ -> Make sure the chosen event type is ‘QRS peak’ -> in Location field choose the ECG signal with the labels
2. Locate any outliers that differ more than 20% from the mean of the 10 values before the outlier (if the outlier is at the beginning of the signal and there are less than 10 data points before it, use 10 intervals after the outlier). To calculate this mean, zoom in on the signal to be able to get the precise measurements -> with the I-beam cursor, mark the fragment of the signal that contains 10 data points before (after) the suspicious outlier -> from the quick measurements, choose ‘Mean’. Then calculate the upper or lower limit (i.e., 1.2 x mean or 0.8 x mean, depending on whether the outlier is higher or lower than the neighboring data points) and compare the suspicious outliers
3. If the interval was ectopic (e.g., a missing beat or missing QRS label), it was removed and interpolated according to Mulder et al., 1992
4. Plot the raw tachogram again to ensure no artifacts remained
5. Before running the analysis, set the parameters. Go to Analysis -> HRV and RSA -> Single epoch HRV spectral. Make sure the method to locate the QRS complexes is set to ‘Events’ -> Make sure the chosen event type is ‘QRS peak’ and Location is the ECG signal with the labels. Parameters:
 - Spline resampling frequency: 8 Hz
 - Frequency Bands tab:
   - Very low frequency band: 0 to 0.04 Hz
   - Low frequency band: 0.04 to 0.15 Hz
   - High frequency band: 0.15 to 0.4 Hz
   - Very high frequency band: 0.4 to 3 Hz
 - PSD option:
   - Window: Hamming
   - Window size: automatic
   - Overlap length: automatic
   - FFT width: 1024
 - Use linear detrending for each window: check
 - Detrend each segment independently: check
 - Ratio output type: LF + HF
6. Go to Analysis -> HRV and RSA -> Multi-epoch HRV and RSA - Spectral
7. Set the parameters:
 - HRV preset: our8
 - ECG Channel: default
 - Extract HRV and RSA for: Periodic time intervals
 - Epoch width: 10 seconds
 - Start first epoch at: beginning of graph
 - Time between epochs: 0 seconds
 - Output type: Text Only
8. Repeat the same analysis with all the epoch widths
9. Repeat for the statistical measures

