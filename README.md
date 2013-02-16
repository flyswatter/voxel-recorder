#Voxel Recorder#
##A module for recording motion and events through time in Voxel.js##

###Example
	var recorder = require('voxel-recorder')
	recorder.register(voxelSkinA, recordingMethod, playbackMethod)

	function recordingMethod(actor){
		return actor.leftArm.position
	}

	function playbackMethod(actor, positionData){
		actor.leftArm.position = positionData
	}

	//Call the tick function each render cycle:
	function renderTick(){
		recorder.tick()
	}

	//Start and stop recording like this:
	recorder.startRecording()
	recorder.stopRecording()

	//When done recording, play it back.
	//Make sure you aren't updating the position
	//With any other methods:
	recorder.jumpToTime(0)
	recorder.loop(true)
	recorder.startPlayback()

##API##
###register(actor, recordingCallback, playbackCallback)
Registers an actor with a callback for recording and playing back.

	function recordingCallback(actor){

		//Includes a reference to the recorded actor.
		//You should return an object that your actor will use
		//to reenact its current position.
		return actor.leftArm.position
	}

	function playbackMethod(actor, positionData){
		//Includes a reference both to the actor and the positionData object you provided.
		//Just plug it together!
		actor.leftArm.position = positionData
	}

###startRecording()

###stopRecording()

###recordingLength()
Returns recording length in milliseconds.

###keyframeCount()
Returns number of significant recorded moments, organized by timestamp.

###currentFrame()
Returns current time stamp in milliseconds.

###jumpToTime(milliseconds)
Calls all actors' playback callbacks at the specified time.

###jumpToKeyframe(keyFrameInteger)
Calls all actors' playback callbacks at the specified keyframe.

###startPlayback()
Begins calling back actors' playback callbacks from the current keyframe.

###pausePlayback()

###loop(boolean)
Whether or not the animation should loop when completing.

###resetPlayback()

###playbackSpeed(speed)
A positive or negative number representing the speed at which to play back when playing.

###clearRecording()

###tick()
Must be called each frame for animation to be captured or performances to be displayed.

###frameSafe(bool)
Tells playback engine whether to render every frame regardless of time or not.  Defaults to false, preserving timing accuracy.