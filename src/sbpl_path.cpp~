/*
  sbpl_path: ROS node for invoking Real Time A* path planner from SBPL
  Copyright (C) 2015-16  Sugandha Sangal

  This program is free software; you can redistribute it and/or
  modify it under the terms of the GNU General Public License
  as published by the Free Software Foundation; either version 2
  of the License, or (at your option) any later version.

  This program is distributed in the hope that it will be useful,
  but WITHOUT ANY WARRANTY; without even the implied warranty of
  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
  GNU General Public License for more details.

  You should have received a copy of the GNU General Public License
  along with this program; if not, write to the Free Software
  Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301, USA.
*/

#include <ros/ros.h>
//#include <ipc_bridge/ipc_bridge.h>
#include <string>
//#include <ipc_bridge/msgs/nav_msgs_Path.h>
//#include <ipc_bridge/msgs/geometry_msgs_PoseStamped.h>
#include <sbpl/headers.h>
#include <geometry_msgs/PoseStamped.h>
#include <geometry_msgs/PoseArray.h>
#include <nav_msgs/Path.h>
#include <nav_msgs/Odometry.h>
#include <cmath>
#include <cstring>
#include <iostream>
#include <vector>


int main(int argc, char** argv){
    ros::init(argc, argv, "sbpl_path") ;
    ros::NodeHandle n("~");
    ros::Publisher sbpl_pub = n.advertise<geometry_msgs::PoseArray>("/path", 50);
   // ros::Publisher sbpl_pub;
    
    //ROS_INFO_STREAM("Hello, ROS! ") ;
    
    ros::Rate r(200.0);
    while(n.ok()){
    ros::spinOnce();
    
    geometry_msgs::PoseArray path;
    path.header.seq = 1;
    path.header.stamp = ros::Time::now();
    path.header.frame_id = "sbpl_path";
    
    geometry_msgs::Pose ps;
    
    //ps.header.seq = 1;
    //ps.header.stamp = ros::Time::now();
    //ps.header.frame_id = "sbpl_path";

    //ps.pose.position.x = 1.0;
    //ps.pose.position.y = 2.0;
    //ps.pose.position.z = 3.0;
    
    //ps.pose.orientation.x = 1.0;
    //ps.pose.orientation.y = 2.0;
    //ps.pose.orientation.z = 3.0;
    //ps.pose.orientation.w = 3.0;
    
    ps.position.x = 1.0;
    ps.position.y = 2.0;
    ps.position.z = 3.0;
    
    ps.orientation.x = 1.0;
    ps.orientation.y = 2.0;
    ps.orientation.z = 3.0;
    ps.orientation.w = 3.0;
    

    
    path.poses.push_back(ps);
    
    sbpl_pub.publish(path);
    
    r.sleep();
    }
    
    return EXIT_SUCCESS;
}
