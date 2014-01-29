Team1880
========

RobotDrive test1
/*----------------------------------------------------------------------------*/
/* Copyright (c) FIRST 2008. All Rights Reserved.                             */
/* Open Source Software - may be modified and shared by FRC teams. The code   */
/* must be accompanied by the FIRST BSD license file in the root directory of */
/* the project.                                                               */
/*----------------------------------------------------------------------------*/
//http://wpilib.screenstepslive.com/s/3120/m/7885/l/79459-the-hello-world-of-frc-robot-programming#!prettyPhoto
package org.ehtp.team1880;


import edu.wpi.first.wpilibj.Joystick;
import edu.wpi.first.wpilibj.SimpleRobot;
import edu.wpi.first.wpilibj.Talon;
import edu.wpi.first.wpilibj.RobotDrive;
import edu.wpi.first.wpilibj.Timer;
/**
 * The VM is configured to automatically run this class, and to call the
 * functions corresponding to each mode, as described in the SimpleRobot
 * documentation. If you change the name of this class or the package after
 * creating this project, you must also update the manifest file in the resource
 * directory.
 */
public class Robot1 extends SimpleRobot {
    Joystick leftStick  = new Joystick(1);
    Joystick rightStick  = new Joystick(2); 
    Talon d_frontRightTalon;
    Talon d_frontLeftTalon;
    Talon d_rearRightTalon;
    Talon d_rearLeftTalon;
    RobotDrive drive = new RobotDrive(1, 2);
    Joystick d_driveJoystick;

    public Robot1() {
        super();

        d_frontRightTalon = new Talon(1);
        d_frontLeftTalon  = new Talon(2);
        d_rearRightTalon  = new Talon(3);
        d_rearLeftTalon   = new Talon(4);

        d_driveJoystick   = new Joystick(1);
    }

    /**
     * This function is called once each time the robot enters autonomous mode.
     */
    public void autonomous() {
       getWatchdog().setEnabled(true);
       getWatchdog().setExpiration(0.5);
       drive.setSafetyEnabled(false); 
       drive.drive(-0.5, 0.0);
       Timer.delay(2.0);
       drive.drive(0.0, 0.0);
       
        for (int i = 0; i < 4; i++) { 
        drive.drive(0.5, 0.0); // drive 50% fwd 0% turn 
        Timer.delay(2.0); // wait 2 seconds 
        drive.drive(0.0, 0.75); // drive 0% fwd, 75% turn 
 } 
        //drive.drive(0.0, 0.0); // drive 0% forward, 0% turn 
        // disable safety on the Talons (write a function that does this)
        // move forward for 2 seconds
        // stop for 2 seconds
        // move backwards for 2 seconds
    }

    /**
     * This function is called once each time the robot enters operator control.
     */
    public void operatorControl() {
        drive.setSafetyEnabled(true);
        while (isOperatorControl() && isEnabled()) {
            drive.tankDrive (leftStick, rightStick);
            Timer.delay(0.01);
        }
        while (true && isOperatorControl() && isEnabled()) // loop until change 
 { 
        drive.tankDrive(leftStick, rightStick); // drive with joysticks 
        Timer.delay(0.005); 
 } 
           
        // Add the loop back from the sample code

        // Make the loop move forward/backward based on how far forward/backward
        // joystick is.  Don't worry about turning yet.  Use just one joystick

        // You'll need to get the value of the joystick each time. (Look at the
        // javadoc for Joystick
    }

    /**
     * This function is called once each time the robot enters test mode.
     */
    public void test() {

    }

    /**
     * Drives the robot forward/backwards at the specified 'speed'.
     * @param speed Value between -1.0 and 1.0
     */
    public void driveFrontBack(double speed) {
        d_frontRightTalon.set(-1.0 * speed);
        d_frontLeftTalon.set(1.0 * speed);
        d_rearRightTalon.set(1.0 * speed);
        d_rearLeftTalon.set(-1.0 * speed);
    }

    // TODO: Write a drive function that takes all the inputs from the joystick
    // and drives based on that.  This includes x, y axis and magnitude and
    // rotational.

    /**
     * Stop the robot
     */
    public void stopRobot() {
        d_frontRightTalon.set(0);
        d_frontLeftTalon.set(0);
        d_rearRightTalon.set(0);
        d_rearLeftTalon.set(0);
    }
}




