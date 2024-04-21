# Spectrum Painter
This code creates a MATLAB App that allows users to generate a spectrogram of an image or QR code with added white noise. The app provides two input options: users can either upload an image file or enter text to create a QR code. Once an input is provided, the app displays the image or QR code and generates a spectrogram of it with added white noise based on the specified signal-to-noise ratio (SNR) value. The spectrogram is a visualization of the frequency content of the signal over time.

In the UIFigure, the user can specify the input type using a radio button group that contains two options: "Image File" and "QR Code Text". The text box for QR code text is shown only when the "QR Code Text" radio button is selected. The image file path text box is provided to allow the user to upload the image file. The app generates a spectrogram using the loaded image and the SNR value entered by the user.

The "SNR (dB)" text box allows the user to specify the desired signal-to-noise ratio. Once the user hits the "Transmit" button, the loaded image or generated QR code along with the spectrogram appears in the UI. The original image or QR code is displayed on the left side while the spectrogram is on the right side.

The resulting spectrogram is displayed as a 3D waterfall plot with time on the x-axis, frequency on the y-axis, and the power spectral density represented by color. The "shading flat" command ensures that each mesh line segment and face has a constant color.


Disclaimer for Regulatory Licensing
===================================
This app should not be used to transmit electromagnetic signals that violate local or federal radiation law.  When transmitting electromagnetic waves with unlicensed devices in the United States, the operator must adhere to FCC regulations.  The ISM band which can be used for low-power transmission is controlled under FCC Part 15.  The first iteration of this project was done in a EE6900 course at Kennesaw State University to show how an SDR can be used to transmit information in a manner different than traditional signal generators.  To test this ability in a real-world scenario, it is imperative that federal, state, and local regulations are followed.


How to edit the .mlapp file?
============================
1. Open MATLAB and navigate to the .mlapp file you want to edit.
2. Double-click on the file to open it in MATLAB App Designer.
3. Once the file is open, you should be able to see both the design view and the code view of the app.
4. If you wish to make any changes to the design of the app, switch to the Design View tab, where you can modify things like the layout, UI components, and properties.
5. If you want to make changes to the code of the app, switch to the Code View tab. Here, you can modify the app's behavior and functionality by writing code.
6. Make the necessary changes to the file.
7. Save your changes by clicking on the Save icon or File > Save.
8. Once you have finished making changes, close the file by clicking on the Close icon or File > Close.


What are the limitations?
=========================
The QR code generation is done through an online API and will not work without internet access.  MATLAB does not have an up-to-date library for generating a QR code.
The parameters of the spectrogram() function are not adjustable in the same way a spectrum analyzer is.


What to add to the file?
========================
The ability to control signal analysis parameters, such as resolution bandwidth or center frequency from the UI would be nice.