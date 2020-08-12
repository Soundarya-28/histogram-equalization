# histogram-equalization.
// Read the image file
Mat image = imread("D:/My OpenCV Website/fly-agaric.jpg");

// Check for failure
if (image.empty())
{
    cout << "Could not open or find the image" << endl;
    cin.get(); //Wait for any key press
    return -1;
}
The above code segment loads the image from the specified file. If it is failed to load the image, the program will exit.


//Convert the image from BGR to YCrCb color space
Mat hist_equalized_image;
cvtColor(image, hist_equalized_image, COLOR_BGR2YCrCb);
The loaded image is in BGR color space. None of the 3 channels (blue, green and red) of this color space cannot be processed to equalize the histogram because all the channels contain color information. Therefore the loaded image should be converted to the YCrCb color space. In this color space, Y channel only contains intensity information while Cr and Cb channels contain color information. Therefore only the Y channel needs to be processed in order to equalize the histogram.


//Split the image into 3 channels; Y, Cr and Cb channels respectively and store it in a std::vector
vector<Mat> vec_channels;
split(hist_equalized_image, vec_channels); The above OpenCV function splits the 3 channel image into 3 separate matrices. Each matrix is pushed to the std::vector. vec_channels[0] contains the Y channel, vec_channels[1] contains the Cr channel and vec_channels[2] contains the Cb channel.


//Equalize the histogram of the Y channel 
equalizeHist(vec_channels[0], vec_channels[0]);The above function equalizes the histogram of the Y channel.


//Merge 3 channels in the vector to form the color image in YCrCB color space.
merge(vec_channels, hist_equalized_image); The above function performs the reverse operation of the split function. It takes a std::vector which consists of 3 matrices representing Y, Cr and Cb channels and creates a 3 channel image in YCrCb color space.


//Convert the histogram equalized image from YCrCb to BGR color space again
cvtColor(hist_equalized_image, hist_equalized_image, COLOR_YCrCb2BGR);Above line converts the image in YCrCb color space into the BGR color space. This step is necessary because OpenCV functions like cv::imshow() always expect images in BGR color space.


//Define the names of windows
String windowNameOfOriginalImage = "Original Image"; 
String windowNameOfHistogramEqualized = "Histogram Equalized Color Image";

// Create windows with the above names
namedWindow(windowNameOfOriginalImage, WINDOW_NORMAL);
namedWindow(windowNameOfHistogramEqualized, WINDOW_NORMAL);
imshow(windowNameOfOriginalImage, image);
imshow(windowNameOfHistogramEqualized, hist_equalized_image);The above code segment will create windows and show images in them. As both windows are created passing the flag WINDOW_NORMAL, they can be resized freely.
waitKey(0); 
destroyAllWindows(); 
return 0;The program will wait until any key is pressed. After a key is pressed, all created windows will be destroyed and the program will exit.

return 0;The program will wait until any key is pressed. 
