# Phusion Passenger: Faye WebSocket demo

This application demonstrates WebSocket support in [the Phusion Passenger application server for Ruby](https://www.phusionpassenger.com/), through the use of the awesome [faye-websocket gem](https://github.com/faye/faye-websocket-ruby). Passenger supports all major modern web technologies, such as WebSockets, entirely out of the box. You don't have to do anything: WebSocket support just works.

If you like this demo, please [tweet about it](https://twitter.com/share) or [follow us on Twitter](https://twitter.com/phusion_nl).

**Table of contents**

 * [Getting started](#getting_started)
 * [Notes](#notes)
 * [Next steps](#next_steps)
 * [About Phusion Passenger](#about)

<center><img src="http://blog.phusion.nl/wp-content/uploads/2012/07/Passenger_chair_256x256.jpg" width="150" height="150" alt="Phusion Passenger"></center>

-------------------------------------------------------

<a name="getting_started"></a>
## Getting started

### Preparations

 1. [Install Phusion Passenger](https://www.phusionpassenger.com/) 4.0.43 or later.
 2. Clone this repository:

        git clone https://github.com/phusion/passenger-ruby-faye-websocket-demo.git
        cd passenger-ruby-faye-websocket-demo

 3. Install dependencies:

        bundle install

### Running the demo in Passenger Standalone

Run:

    passenger start

Access the demo application at http://0.0.0.0:3000/ and see it in action.

### Running the demo in Passenger for Nginx

Create a virtual host in your Nginx configuration file:

    server {
        listen 3000;
        server_name passenger-ruby-faye-websocket.demo;
        root /path-to/passenger-ruby-faye-websocket-demo/public;
        passenger_enabled on;
    }

Add `passenger-ruby-faye-websocket.demo` to your `/etc/hosts`:

    echo 127.0.0.1 passenger-ruby-faye-websocket.demo | sudo tee -a /etc/hosts

Then restart Nginx, and access the demo application at http://passenger-ruby-faye-websocket.demo:3000/

### Running the demo in Passenger for Apache

Apache itself doesn't work very well with WebSockets, so running in Apache is not recommended. Having said that, Socket.io gracefully falls back to polling when run on Apache, so the demo still works.

Create a virtual host in your Apache configuration file:

    # Comment out if you already have a "Listen 3000" directive somewhere.
    Listen 3000
    # Comment out when using Apache >= 2.4.
    NameVirtualHost *:3000

    <VirtualHost *:3000>
        ServerName passenger-ruby-faye-websocket.demo
        DocumentRoot /path-to/passenger-ruby-faye-websocket-demo/public
    </VirtualHost>

Add `passenger-ruby-faye-websocket.demo` to your `/etc/hosts`:

    echo 127.0.0.1 passenger-ruby-faye-websocket.demo | sudo tee -a /etc/hosts

Then restart Apache, and access the demo application at http://passenger-ruby-faye-websocket.demo:3000/

<a name="notes"></a>
## Notes

### Multithreading not required

WebSockets works great on both the open source variant of Phusion Passenger, as well as on [Phusion Passenger Enterprise](https://www.phusionpassenger.com/). Multithreading is *not* required for faye-websocket to work optimally, because faye-websocket uses EventMachine to serve WebSockets.

### Non-Faye demo

There is also a Phusion Passenger + WebSocket demo that does not use the faye-websocket gem: https://github.com/phusion/passenger-ruby-websocket-demo. That demo is implemented using pure Rack and a low-level WebSocket parser library, showing you how things might work if you use WebSockets through a different gem.

<a name="next_steps"></a>
## Next steps

 * Using WebSockets on Phusion Passenger? [Tweet about us](https://twitter.com/share), [follow us on Twitter](https://twitter.com/phusion_nl) or [fork us on Github](https://github.com/phusion/passenger).
 * Having problems? Please post a message at [the community discussion forum](https://groups.google.com/d/forum/phusion-passenger).

[<img src="http://www.phusion.nl/assets/logo.png">](http://www.phusion.nl/)

Please enjoy Phusion Passenger, a product by [Phusion](http://www.phusion.nl/). :-)

<a name="about"></a>
## About Phusion Passenger

<a href="http://vimeo.com/phusionnl/review/80475623/c16e940d1f"><img src="http://blog.phusion.nl/wp-content/uploads/2014/05/GameOfThronesVideo.png" height="300"></a><br><em>Phusion Passenger used in Game of Thrones Ascention</em>

[Phusion Passenger™](https://www.phusionpassenger.com/) is a web server and application server, designed to be fast, robust and lightweight. It takes a lot of complexity out of deploying web apps, adds powerful enterprise-grade features that are useful in production, and makes administration much easier and less complex. Phusion Passenger supports Ruby, Python, Node.js and Meteor, and is being used by high-profile companies such as **Apple, Pixar, New York Times, AirBnB, Juniper** etc as well as [over 350.000 websites](http://trends.builtwith.com/Web-Server/Phusion-Passenger).

**Learn more:** [Website](https://www.phusionpassenger.com/) | [Documentation](https://www.phusionpassenger.com/documentation_and_support) | [Support resources](https://www.phusionpassenger.com/documentation_and_support) | [Github](https://github.com/phusion/passenger) | [Twitter](https://twitter.com/phusion_nl) | [Blog](http://blog.phusion.nl/)
