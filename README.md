
```
sudo apt install cmake libevdev-dev libudev-dev libconfig++-dev
mkdir ~/build
cd build
git clone https://github.com/horschte/logitech-mx-master-3
cmake logitech-mx-master-3
make
sudo make install
sudo nano /etc/logid.cfg
```
```
devices: (
    {
        name: "Wireless Mouse MX Master 3";
        dpi: 2000;
        smartshift:
        {
            on: true;
            threshold: 20;
        };
        hiresscroll:
        {
            hires: true;
            invert: false;
            target: false;
        };
    thumbwheel:
    {
        divert: true;
        invert: false;
        
        left:
        {
            threshold: 1;
            interval: 25;

            direction: "Left";
            mode: "OnInterval";
        action =
        {
            type: "Keypress";
keys: ["KEY_LEFTCTRL", "KEY_LEFTALT", "KEY_DOWN"];
        };

        };

    right: {
        threshhold: 1;
        interval: 25;
        direction: "Right";
        mode: "OnInterval";
        action =
                { 
                type: "Keypress";
                keys: ["KEY_LEFTCTRL","KEY_LEFTSHIFT", "KEY_0"]
                };
    };

    };
        buttons: (
            {
                cid: 0xc3;
                action =
                {
                    type: "Gestures";
                    gestures: (
                        { direction: "Left";  mode: "OnRelease"; action = { type: "Keypress"; keys: ["KEY_LEFTCTRL", "KEY_PAGEUP"]; }; },
                        { direction: "Right"; mode: "OnRelease"; action = { type: "Keypress"; keys: ["KEY_LEFTCTRL", "KEY_PAGEDOWN"]; }; },
                        { direction: "None"   mode: "NoPress" }
                    );
                };
            },
            {
                cid: 0xc4;
		action = { type: "CycleDPI"; dpis: [400, 1000, 1600]; }; 
            },
            {
                cid: 0x53;
                action = { type :  "Keypress"; keys: ["KEY_LEFTCTRL", "KEY_V"]; };
            },
            {
                cid: 0x56;
                action = { type :  "Keypress"; keys: ["KEY_LEFTCTRL", "KEY_C"]; };
            }
        );
    }
    );
```
```
systemctl enable logid
systemctl start logid
```
