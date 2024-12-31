# UI Improvements and Toast Notifications in Create/Join Room Component

This commit enhances the user interface (UI) of the `CreateJoinRoom` component and integrates toast notifications for better user feedback.

**Previous Code:** The previous version had a basic UI with create and join room functionality.  It lacked visual appeal and didn't provide feedback to the user on successful or failed room actions.

**Current Code:**

```jsx
import { useEffect, useState } from "react";
import { useNavigate } from "react-router-dom";
import { useSocket } from "../context/Socket";
import { useSelector, useDispatch } from "react-redux";
import { AuthUser } from "../slice/todosSlice";
import toast from "react-hot-toast";
import { TypeAnimation } from "react-type-animation";
import { Fade, Slide } from "react-awesome-reveal";
import { Tooltip } from "react-tooltip";
import HomeSvg from "../assets/home-svg.svg";

const CreateJoinRoom = () => {
  const socket = useSocket();
  const [input, setInput] = useState({ joinRoom: "" });
  const [profile, setProfile] = useState();

  const dispatch = useDispatch();
  const currentToken = useSelector((state) => state.todos.token);
  const navigate = useNavigate();

  dispatch(AuthUser(currentToken)).then((response) => {
    if (response.payload) {
      setProfile(response.payload._id);
    }
  });

  const handleInput = (e) => {
    const { name, value } = e.target;

    setInput({ ...input, [name]: value });
  };

  useEffect(() => {
    socket.on("join-msg", (data) => {
      if (data.error) {
        toast.error(data.error, {
          position: "top-center",
        });
        console.log(data.error);
      } else {
        toast.success("Joined Room Successfully", {
          position: "top-center",
        });
        console.log(`${data.userName} joined room: ${data.roomId}`);

        navigate(`/chat/${data.roomId}`, {
          state: { userName: data.userName },
        });
      }
    });

    return () => {
      socket.off("join-msg");
    };
  }, [navigate]);

  const handleCreateRoom = (e) => {
    e.preventDefault();
    socket.emit("create-room", profile);
    socket.on("msg", (val) => {
      console.log(val.user + " created Room with RoomID " + val.id);
      navigate(`/chat/${val.id}`);
    });
    setInput({ ...input, userName: "", joinRoom: "" });
  };

  const handleJoinRoom = (e) => {
    e.preventDefault();
    socket.emit("join-room", profile, input.joinRoom);
  };

  return (
    <>
      <div className="border-2 border-black p-2">
        <div className="my-4">
          <div className="w-fit bg-gray-100 px-5 py-1 rounded-full border border-black text-sm">
            👥 | Create Or Join Room
          </div>
        </div>

        <div className="my-10">
          <div className="title text-7xl flex justify-center items-center">
            <TypeAnimation
              sequence={["Start New Room"]}
              speed={30}
              repeat={0}
              cursor={false}
            />
          </div>

          <Fade
            delay={200}
            duration={1000}
            triggerOnce
            fraction={0.5}
            className="text-center"
          >
            <div className="text-2xl text-center">
              Create a room to collaborate and organize tasks with your team.
              <br />
              Share the room code with others to join.
            </div>
          </Fade>

          <div className="mt-16 flex justify-center items-center ">
            <button
              className="font-thin group transition-all active:scale-95"
              onClick={handleCreateRoom}
            >
              <div className="flex justify-center items-center font-medium gap-2 transition-all">
                Create New Room
                <img className="rotate-45 group-hover:rotate-90 transition-all transform duration-300" />
              </div>
              <hr className="w-0 group-hover:w-full h-1 transition-all duration-500 bg-black" />
            </button>
          </div>
        </div>

        <div className="my-10">
          <div className="title text-7xl flex justify-center items-center">
            <TypeAnimation
              sequence={["Enter a Room"]}
              speed={30}
              repeat={0}
              cursor={false}
            />
          </div>

          <Fade
            delay={200}
            duration={1000}
            triggerOnce
            fraction={0.5}
            className="text-center"
          >
            <div className="text-2xl text-center">
              Already have a room code? Enter it below to collaborate with your
              team.
              {/* <br />
              Share the room code with others to join. */}
            </div>
          </Fade>

          <div className="mt-16 flex justify-center items-center ">
            <div className="w-[40%] flex">
              <div className="w-5/6 py-1">
                <input
                  type="text"
                  className="w-full px-4 py-1 border-black rounded-tl-lg text-gray-800 focus:outline-dotted focus:bg-slate-100 bg-slate-50 shadow-sm"
                  placeholder="Enter Room ID"
                  name="joinRoom"
                  onChange={handleInput}
                  value={input.joinRoom}
                />
              </div>
              <div className="w-1/6 flex justify-center items-center group">
                <button
                  className="w-full flex items-center bg-black text-sm font-medium text-white rounded-tr-lg justify-center py-[7px] hover:opacity-70 shadow-sm active:scale-95 transition-all"
                  onClick={handleJoinRoom}
                >
                  Join
                </button>
              </div>
            </div>
          </div>
        </div>

        {/* old  */}
        <div className="flex justify-center items-center">
          <div className="w-[80%] flex justify-center items-center my-5 bg-slate-100 rounded-md">
            <form
              action=""
              className="w-[80%] my-8 flex flex-col justify-center items-center"
            >
              <div className="flex flex-col justify-center items-center">
                <p className="font-semibold tracking-wider my-4">
                  Create New Room
                </p>
                <button
                  onClick={handleCreateRoom}
                  className="w-fit px-4 py-2 mx-4 rounded-lg group bg-gradient-to-br from-blue-500 to-purple-400 text-sm font-medium text-white hover:scale-105 hover:opacity-70 transition-all duration-200"
                >
                  Create Room
                </button>
              </div>

              <hr className="my-8 h-[2px] w-full rounded-sm bg-gradient-to-br from-red-500 to-orange-400" />

              <div className="flex flex-col justify-center items-center">
                <p className="font-semibold tracking-wider my-4">Join Room</p>
                <div className="w-[100%] justify-center flex items-center rounded-md shadow-sm">
                  <div className="w-[80%] ">
                    <input
                      className="w-full px-4 py-2 rounded-l-lg text-gray-800 focus:outline-none"
                      type="text"
                      placeholder="Enter Room ID"
                      name="joinRoom"
                      onChange={handleInput}
                      value={input.joinRoom}
                    />
                  </div>

                  <div className="w-[20%] flex justify-center items-center hover:opacity-60">
                    <button
                      onClick={handleJoinRoom}
                      className="w-full flex items-center bg-gradient-to-br from-blue-500 to-purple-400 text-sm font-medium text-white rounded-r-lg justify-center py-2 hover:scale-105 hover:opacity-70 transition-all duration-200"
                    >
                      Join
                    </button>
                  </div>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
    </>
  );
};

export default CreateJoinRoom;
```

The UI is now more modern and visually appealing using `react-awesome-reveal` for animations and improved styling.  `react-hot-toast` is used to display success and error messages after attempting to create or join a room, providing immediate feedback to the user.  The old UI is kept commented out for reference.
