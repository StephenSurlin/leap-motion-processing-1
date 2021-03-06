# Leap Motion for Processing

Simple library to use the complete [Leap Motion](https://leapmotion.com/) [SDK](https://developer.leapmotion.com/documentation/java/index.html) in [Processing](http://processing.org/).


## Table of Contents

- [About](#about)
- [Download](#download)
- [Installation](#installation)
- [Dependencies](#dependencies)
- [Tested](#tested)
- [Examples](#examples)
- [Usage](#usage)
- [Changelog](#changelog)
- [Questions?](#questions)
- [License](#license)


## About

The Leap detects and tracks hands, fingers and finger-like tools. The device operates in an intimate proximity with high precision and tracking frame rate.

The Leap software analyzes the objects observed in the device field of view. It recognizes hands, fingers, and tools, reporting both discrete positions and motion. The Leap field of view is an inverted pyramid centered on the device. The effective range of the Leap extends from approximately 25 to 600 millimeters above the device (1 inch to 2 feet).


## Download

- [Leap Motion for Processing v2.2.3.1](download/LeapMotionForProcessing.zip?raw=true)

Note: If you are interested in the newest **beta** implementation, so have a look at the **dev branch**.


## Installation

Unzip and put the extracted *LeapMotionForProcessing* folder into the libraries folder of your Processing sketches. Reference and examples are included in the *LeapMotionForProcessing* folder. For further help read the [tutorial](http://www.learningprocessing.com/tutorials/libraries/) by [Daniel Shiffman](https://github.com/shiffman).


## Dependencies

- [Leap Motion Software](https://developer.leapmotion.com/) **2.2.3+25971**


## Tested

System:

- **OSX** (*Mac OS 10.7 and higher*)
- **Linux** (*not tested yet, but it should work*) (*Ubuntu Linux 12.04 LTS and Ubuntu 13.04 Raring Ringtail*)
- **Windows** (*not tested yet, but x86 and x64 should work*) (*Windows 7 and 8*)

Processing version:

- **3.0a5**
- **2.2.1**
- 2.1.2
- 2.1.1
- 2.1.0
- 2.0.1
- 2.0b9
- 2.0b8
- 2.0b7

Leap Motion Software version:

* **2.2.3+25971**
* 2.2.1+24116
* 2.2.0+23475
* 2.1.6+23110
* 2.1.5+22699
* 2.0.5+18024 BETA
* 2.0.4+17546 BETA
* 2.0.3+17004 BETA
* 2.0.2+16391 BETA
* 2.0.1+15831 BETA
* 2.0.0+13819 BETA
* ...


## Examples

* [Basic Data-Access](#basic-data-access) → [e1_basic.pde](examples/e1_basic/e1_basic.pde)
* [Gesture-Recognition](#gesture-recognition) → [e2_gestures.pde](examples/e2_gestures/e2_gestures.pde)
* [Camera-Images](#camera-images) → [e3_camera_images.pde](examples/e3_camera_images/e3_camera_images.pde)


## Usage

### Basic Data-Access

Before you start to code I recommend you to read the [official basic introduction](https://developer.leapmotion.com/documentation/java/devguide/Leap_Overview.html).

```java
import de.voidplus.leapmotion.*;

LeapMotion leap;

void setup(){
    size(800, 500, OPENGL);
    background(255);
    // ...

    leap = new LeapMotion(this);
}

void draw(){
    background(255);
    // ...
    int fps = leap.getFrameRate();


    // ========= HANDS =========

    for(Hand hand : leap.getHands()){


        // ----- BASICS -----

        int     hand_id          = hand.getId();
        PVector hand_position    = hand.getPosition();
        PVector hand_stabilized  = hand.getStabilizedPosition();
        PVector hand_direction   = hand.getDirection();
        PVector hand_dynamics    = hand.getDynamics();
        float   hand_roll        = hand.getRoll();
        float   hand_pitch       = hand.getPitch();
        float   hand_yaw         = hand.getYaw();
        boolean hand_is_left     = hand.isLeft();
        boolean hand_is_right    = hand.isRight();
        float   hand_grab        = hand.getGrabStrength();
        float   hand_pinch       = hand.getPinchStrength();
        float   hand_time        = hand.getTimeVisible();
        PVector sphere_position  = hand.getSpherePosition();
        float   sphere_radius    = hand.getSphereRadius();


        // ----- SPECIFIC FINGER -----

        Finger  finger_thumb     = hand.getThumb();
        // or                      hand.getFinger("thumb");
        // or                      hand.getFinger(0);

        Finger  finger_index     = hand.getIndexFinger();
        // or                      hand.getFinger("index");
        // or                      hand.getFinger(1);

        Finger  finger_middle    = hand.getMiddleFinger();
        // or                      hand.getFinger("middle");
        // or                      hand.getFinger(2);

        Finger  finger_ring      = hand.getRingFinger();
        // or                      hand.getFinger("ring");
        // or                      hand.getFinger(3);

        Finger  finger_pink      = hand.getPinkyFinger();
        // or                      hand.getFinger("pinky");
        // or                      hand.getFinger(4);


        // ----- DRAWING -----

        hand.draw();
        // hand.drawSphere();


        // ========= ARM =========

        if(hand.hasArm()){
            Arm     arm               = hand.getArm();
            float   arm_width         = arm.getWidth();
            PVector arm_wrist_pos     = arm.getWristPosition();
            PVector arm_elbow_pos     = arm.getElbowPosition();
        }


        // ========= FINGERS =========

        for(Finger finger : hand.getFingers()){


            // ----- BASICS -----

            int     finger_id         = finger.getId();
            PVector finger_position   = finger.getPosition();
            PVector finger_stabilized = finger.getStabilizedPosition();
            PVector finger_velocity   = finger.getVelocity();
            PVector finger_direction  = finger.getDirection();
            float   finger_time       = finger.getTimeVisible();


            // ----- SPECIFIC FINGER -----

            switch(finger.getType()){
                case 0:
                    // System.out.println("thumb");
                    break;
                case 1:
                    // System.out.println("index");
                    break;
                case 2:
                    // System.out.println("middle");
                    break;
                case 3:
                    // System.out.println("ring");
                    break;
                case 4:
                    // System.out.println("pinky");
                    break;
            }


            // ----- SPECIFIC BONE -----

            Bone    bone_distal       = finger.getDistalBone();
            // or                       finger.get("distal");
            // or                       finger.getBone(0);

            Bone    bone_intermediate = finger.getIntermediateBone();
            // or                       finger.get("intermediate");
            // or                       finger.getBone(1);

            Bone    bone_proximal     = finger.getProximalBone();
            // or                       finger.get("proximal");
            // or                       finger.getBone(2);

            Bone    bone_metacarpal   = finger.getMetacarpalBone();
            // or                       finger.get("metacarpal");
            // or                       finger.getBone(3);


            // ----- DRAWING -----

            // finger.draw(); // = drawLines()+drawJoints()
            // finger.drawLines();
            // finger.drawJoints();


            // ----- TOUCH EMULATION -----

            int     touch_zone        = finger.getTouchZone();
            float   touch_distance    = finger.getTouchDistance();

            switch(touch_zone){
                case -1: // None
                    break;
                case 0: // Hovering
                    // println("Hovering (#"+finger_id+"): "+touch_distance);
                    break;
                case 1: // Touching
                    // println("Touching (#"+finger_id+")");
                    break;
            }
        }


        // ========= TOOLS =========

        for(Tool tool : hand.getTools()){


            // ----- BASICS -----

            int     tool_id           = tool.getId();
            PVector tool_position     = tool.getPosition();
            PVector tool_stabilized   = tool.getStabilizedPosition();
            PVector tool_velocity     = tool.getVelocity();
            PVector tool_direction    = tool.getDirection();
            float   tool_time         = tool.getTimeVisible();


            // ----- DRAWING -----

            // tool.draw();


            // ----- TOUCH EMULATION -----

            int     touch_zone        = tool.getTouchZone();
            float   touch_distance    = tool.getTouchDistance();

            switch(touch_zone){
                case -1: // None
                    break;
                case 0: // Hovering
                    // println("Hovering (#"+tool_id+"): "+touch_distance);
                    break;
                case 1: // Touching
                    // println("Touching (#"+tool_id+")");
                break;
            }
        }
    }


    // ========= DEVICES =========

    for(Device device : leap.getDevices()){
        float device_horizontal_view_angle = device.getHorizontalViewAngle();
        float device_verical_view_angle = device.getVerticalViewAngle();
        float device_range = device.getRange();
    }

}

// ========= CALLBACKS =========

void leapOnInit(){
    // println("Leap Motion Init");
}
void leapOnConnect(){
    // println("Leap Motion Connect");
}
void leapOnFrame(){
    // println("Leap Motion Frame");
}
void leapOnDisconnect(){
    // println("Leap Motion Disconnect");
}
void leapOnExit(){
    // println("Leap Motion Exit");
}
```


### Gesture-Recognition

![Snapshot](reference/leap_gestures.jpg)

> Source: [Leap Motion](https://developer.leapmotion.com/documentation/skeletal/java/devguide/Leap_Overview.html#gestures)

```java
import de.voidplus.leapmotion.*;

LeapMotion leap;

void setup(){
    size(800, 500, OPENGL);
    background(255);
    // ...

    leap = new LeapMotion(this).withGestures();
    // leap = new LeapMotion(this).withGestures("circle, swipe, screen_tap, key_tap");
    // leap = new LeapMotion(this).withGestures("swipe"); // Leap detects only swipe gestures.
}

void draw(){
    background(255);
    // ...
}


// ----- SWIPE GESTURE -----

void leapOnSwipeGesture(SwipeGesture g, int state){
	int 	id 					= g.getId();
	Finger	finger 				= g.getFinger();
	PVector	position 			= g.getPosition();
	PVector position_start 		= g.getStartPosition();
	PVector direction 			= g.getDirection();
	float 	speed 				= g.getSpeed();
	long 	duration 			= g.getDuration();
    float   duration_seconds 	= g.getDurationInSeconds();

	switch(state){
		case 1:	// Start
			break;
		case 2: // Update
			break;
		case 3: // Stop
			println("SwipeGesture: "+id);
			break;
	}
}


// ----- CIRCLE GESTURE -----

void leapOnCircleGesture(CircleGesture g, int state){
	int 	id 					= g.getId();
	Finger	finger 				= g.getFinger();
	PVector	position_center 	= g.getCenter();
	float	radius 				= g.getRadius();
	float 	progress 			= g.getProgress();
	long 	duration 			= g.getDuration();
	float 	duration_seconds 	= g.getDurationInSeconds();
    int     direction          = g.getDirection();

	switch(state){
		case 1:	// Start
			break;
		case 2: // Update
			break;
		case 3: // Stop
			println("CircleGesture: "+id);
			break;
	}

    switch(direction){
        case 0: // Anticlockwise/Left gesture
            break;
        case 1: // Clockwise/Right gesture
            break;
    }
}


// ----- SCREEN TAP GESTURE -----

void leapOnScreenTapGesture(ScreenTapGesture g){
	int 	id 					= g.getId();
	Finger	finger 				= g.getFinger();
	PVector	position			= g.getPosition();
	PVector direction			= g.getDirection();
	long 	duration 			= g.getDuration();
	float 	duration_seconds 	= g.getDurationInSeconds();

	println("ScreenTapGesture: "+id);
}


// ----- KEY TAP GESTURE -----

void leapOnKeyTapGesture(KeyTapGesture g){
	int 	id 					= g.getId();
	Finger	finger 				= g.getFinger();
	PVector	position			= g.getPosition();
	PVector direction			= g.getDirection();
	long 	duration 			= g.getDuration();
	float 	duration_seconds 	= g.getDurationInSeconds();

	println("KeyTapGesture: "+id);
}
```

### Camera-Images

```java
import de.voidplus.leapmotion.*;

LeapMotion leap;

void setup(){
	size(640, 480, OPENGL);
	background(255);  
	leap = new LeapMotion(this);
}

void draw(){
	background(255);

	// ========= CAMERA IMAGES =========

	if (leap.hasImages()) {
		for (Image camera : leap.getImages()) {
			if (camera.isLeft()) {
				// left camera
				image(camera, 0, 0);
			} else {
				// right camera
				image(camera, 0, camera.getHeight());
			}
		}
	}

}
```


## Changelog

### v2.2.3.1

- Added support for SDK 2.2.3+25971
	- Updated libraries

### v2.2.2.1

- Added support for SDK 2.2.2+24469
	- Updated libraries

### v2.2.1.1

- Added support for SDK 2.2.1+24116
	- Updated libraries
- Changed public methods:
	- Class ```LeapMotion```
		- ```ArrayList<Finger> getOutstretchedFingers()```
	- Class ```Hand```
		- ```ArrayList<Finger> getOutstretchedFingers()```
- Added public methods:
	- Class ```LeapMotion```
		- ```ArrayList<Finger> getOutstretchedFingersByAngle()```
		- ```ArrayList<Finger> getOutstretchedFingersByAngle(int similarity)``` [0-100]
	- Class ```Hand```
		- ```ArrayList<Finger> getOutstretchedFingersByAngle()```
		- ```ArrayList<Finger> getOutstretchedFingersByAngle(int similarity)``` [0-100]

Fixed [getOutstretchedFingers() bug](https://twitter.com/harveymoon0/status/546479022687809537) 

### v2.2.1

- Fixed [getType() bug](https://twitter.com/Atlas_Slouched/status/537676868129140736) of fingers in gestures.

### v2.2.0

- Added support for SDK 2.2.0+23475
	- Updated libraries

### v2.1.6

- Added support for SDK 2.1.6+23110
	- Updated libraries
	- Improved [policy handling](https://community.leapmotion.com/t/policyflags-in-java/1941)
- Added public methods:
	- Class ```LeapMotion```
		- ```LeapMotion withBackgroundFrames()```
		- ```LeapMotion withoutBackgroundFrames()```
		- ```LeapMotion withCameraImages()```
		- ```LeapMotion withoutCameraImages()```
		- ```LeapMotion withOptimizedHdm()```
		- ```LeapMotion withoutOptimizedHdm()```
		- ```void printPolicyFlags()```
- Added public methods:
	- Class ```LeapMotion```
		- ```LeapMotion allowRunInBackground()```
- Cleaned up.

### v2.1.5.1

- Added *Image API*
- Added new class:
	- Class ```Image```
- Added public methods:
	- Class ```LeapMotion```
		- ```LeapMotion withCameraImages()```
		- ```boolean hasImages()```
		- ```ArrayList<Image> getImages()```
		- ```LeapMotion withOptimizedHdm()```
	- Class ```Image```
		- ```boolean isValid()```
		- ```int getId()```
		- ```int getWidth()```
		- ```int getHeight()```
		- ```boolean isLeft()```
		- ```boolean isRight()```
- Added new example [e3_camera_images.pde](examples/e3_camera_images/e3_camera_images.pde), which demonstrates the use of the *Image API*

### v2.1.5

- Added support for SDK 2.1.5+22699
	- Updated libraries
- Added public methods:
	- Class ```Arm```
		- ```PVector getPosition()```
		- ```PVector getRawPosition()```
	- Class ```LeapMotion```
		- ```LeapMotion allowRunInBackground()``` ← ```LeapMotion runInBackground()```
- Added public methods:
	- Class ```LeapMotion```
		- Added deprecation message to ```LeapMotion runInBackground()```

### v2.0.5 BETA

- Added support for SDK 2.0.5+18024 BETA
	- Updated libraries

### v2.0.4.1 BETA

- Added public methods:
	- Class ```LeapMotion```
		- ```ArrayList<Finger> getOutstrechtedFingers()``` (Default: 75%)*
		- ```ArrayList<Finger> getOutstrechtedFingers(int similarity)```*
	- Class ```Hand```
		- ```ArrayList<Finger> getOutstrechtedFingers()``` (Default: 75%)*
		- ```ArrayList<Finger> getOutstrechtedFingers(int similarity)```*

"*" = custom

### v2.0.4 BETA

- Added support for SDK 2.0.4+17546 BETA
	- Updated libraries

### v2.0.3.1 BETA

- Added public methods:
	- Class ```Gesture```
		- ```int getType()``` (-1=NO_GESTURE, 0=TYPE_CIRCLE, 1=TYPE_KEY_TAP, 2=TYPE_SCREEN_TAP, 3=TYPE_SWIPE)
	- Class ```CircleGesture```
		- ```int getDirection()``` (0=anticlockwise/left, 1=clockwise/right)

### v2.0.3 BETA

- Added support for SDK 2.0.3+17004 BETA
	- Updated libraries
- Added new class:
	- Class ```Arm```
- Added public methods:
	- Class ```Arm```
		- ```boolean isValid()```
		- ```PVector getWristPosition()```
		- ```PVector getWristRawPosition()```
		- ```PVector getElbowPosition()```
		- ```PVector getElbowRawPosition()```
		- ```float getWidth()```
	- Class ```Hand```
		- ```Arm getArm()```
		- ```boolean hasArm()```
	- Class ```LeapMotion```
		- ```LeapMotion moveWorld(Integer x, Integer y, Integer z)```
		- ```LeapMotion moveWorld(PVector origin)```

### v2.0.2.2 BETA

- Added public methods:
	- Class ```Hand```
		- ```boolean isValid()```
	- Class ```Bone```
		- ```boolean isValid()```
	- Class ```Finger```
		- ```boolean isValid()```
	- Class ```Tool```
		- ```boolean isValid()```
- Changed public methods:
	- Class ```LeapMotion```
		- ```Hand getHand(Integer id)```
		- ```ArrayList<Hand> getHands()```
		- ```Hand getFrontHand()```
		- ```Hand getLeftHand()```
		- ```Hand getRightHand()```
		- ```Finger getFinger(Integer id)```
		- ```ArrayList<Finger> getFingers()```
		- ```Tool getTool(Integer id)```
		- ```ArrayList<Tool> getTools()```

### v2.0.2 BETA

- Added support for SDK 2.0.2+16391 BETA
	- Updated libraries

### v2.0.1 BETA

- Added support for SDK v2.0.1+15831 BETA
	- Updated libraries
	- Added new Bone API
- Added new class:
	- Class ```Bone```
- Added public methods:
	- Class ```Bone```
		- ```float getLength()```
		- ```float getWidth()```
		- ```PVector getNextJoint()``` and ```PVector getRawNextJoint()```
		- ```PVector getPrevJoint()``` and ```PVector getRawPrevJoint()```
		- ```int getType()``` ([0-3], 0=distal, 1=intermediate, 2=proximal, 3=metacarpal)
		- ```PVector getDirection()``` and ```PVector getRawDirection()```
		- ```void draw()``` and ```void draw(boolean pre)```
	- Class ```Hand```
		- ```float getWidth()```
	- Class ```Finger```
		- ```Bone getBone(int index)``` ([0-3], 0=distal, 1=intermediate, 2=proximal, 3=metacarpal)
		- ```Bone getBone(int name)``` ("distal", "intermediate", "proximal", "metacarpal")
		- ```Bone getDistalBone()```
		- ```Bone getIntermediateBone()```
		- ```Bone getMetacarpalBone()```
		- ```Bone getProximalBone()```
		- ```void drawBones()``` and ```void drawBones(boolean pre)```
	- Class ```LeapMotion```
		- ```long getId()```
		- ```long getTimestamp()```
- Changed public methods:
	- Class ```Finger```
		- ```void draw()```
		- ```void draw(int radius)```
		- ```void draw(boolean pre)```
		- ```void draw(int radius, boolean pre)```
		- ```void drawJoints()```
		- ```void drawJoints(boolean pre)```
		- ```void drawLines()```
		- ```void drawLines(int radius)```
		- ```void drawLines(boolean pre)```
		- ```void drawLines(int radius, boolean pre)```
	- Class ```Hand```
		- ```void draw()```
		- ```void draw(int radius)```
		- ```void draw(boolean pre)```
		- ```void draw(int radius, boolean pre)```
		- ```void drawSphere()```
		- ```void drawSphere(boolean pre)```
		- ```void drawFingers()```
		- ```void drawFingers(int radius)```
		- ```void drawFingers(boolean pre)```
		- ```void drawFingers(int radius, boolean pre)```
- Fixed [Gestures in Processing](https://community.leapmotion.com/t/gestures-in-processing/873/11)

### v2.0.0 BETA

- Added support for SDK v2.0.0+13819 BETA
- Added public methods:
	- Class ```Hand```
		- ```Finger getFinger(int index)``` ([0-4], 0=thumb, 1=index, 2=middle, 3=ring, 4=pinky)
		- ```Finger getFinger(String name)``` ("thumb", "index", "middle", "ring", "pinky")
		- ```Finger getThumb()```
		- ```Finger getIndexFinger()```
		- ```Finger getMiddleFinger()```
		- ```Finger getRingFinger()```
		- ```Finger getPinkyFinger()```
		- ```float getConfidence()```
		- ```boolean isLeft()```
		- ```boolean isRight()```
		- ```float getGrabStrength()``` ([0..1])
		- ```float getPinchStrength()``` ([0..1])
		- ```void drawSphere()```
		- ```void drawFingers()```
	- Class ```Finger```
		- ```PVector getPositionOfJointTip()``` and ```PVector getRawPositionOfJointTip()```
		- ```PVector getPositionOfJointMcp()``` and ```PVector getRawPositionOfJointMcp()```
		- ```PVector getPositionOfJointPip()``` and ```PVector getRawPositionOfJointPip()```
		- ```PVector getPositionOfJointDip()``` and ```PVector getRawPositionOfJointDip()```
		- ```int getType()``` ([0-4], 0=thumb, 1=index, 2=middle, 3=ring, 4=pinky)
		- ```void drawLines()```
		- ```void drawJoints()```
	- Class ```Tool```
		- ```PVector getTipPosition()```
		- ```void draw()```
- Changed public methods:
	- Class ```Hand```
		- ```void draw()```
	- Class ```Finger```
		- ```void draw()```
	- Class ```Tool```
		- ```void draw()```
- Removed public methods:
	- Class ```Finger```
		- ```void drawDirection()```


## Questions?

Don't be shy and feel free to contact me on Twitter: [@darius_morawiec](https://twitter.com/darius_morawiec)


## License

The library is Open Source Software released under the [License](LICENSE.txt).
