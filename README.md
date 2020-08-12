# histogram-equalization.
#include <opencv2/opencv.hpp>
#include <iostream>

using namespace cv;
using namespace std;

int main(int argc, char** argv)
{
    Mat image = imread("D:/My OpenCV Website/fly-agaric.jpg");
    if (image.empty())
    {
        cout << "Could not open or find the image" << endl;
        cin.get(); //wait for any key press
        return -1;
    }
    Mat hist_equalized_image;
    cvtColor(image, hist_equalized_image, COLOR_BGR2YCrCb);
    vector<Mat> vec_channels;
    split(hist_equalized_image, vec_channels); 
    equalizeHist(vec_channels[0], vec_channels[0]);
    merge(vec_channels, hist_equalized_image); 
      cvtColor(hist_equalized_image, hist_equalized_image, COLOR_YCrCb2BGR);
    String windowNameOfOriginalImage = "Original Image"; 
    String windowNameOfHistogramEqualized = "Histogram Equalized Color Image";

 
 namedWindow(windowNameOfOriginalImage, WINDOW_NORMAL);
    namedWindow(windowNameOfHistogramEqualized, WINDOW_NORMAL);
    imshow(windowNameOfOriginalImage, image);
    imshow(windowNameOfHistogramEqualized, hist_equalized_image);
    waitKey(0); 
    destroyAllWindows(); 
    return 0;
}
