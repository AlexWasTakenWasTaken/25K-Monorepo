# 25K-Monorepo

<h2>Key Algorithms and Structures</h2>

<h3>1. Median Filtering</h3>
<p>
  In <code>okapi/api/filter/medianFilter.hpp</code>, there is a template-based <em>MedianFilter</em> class. This filter
  applies a median-based smoothing technique to sensor readings or other data values. By taking a fixed window of values
  (taps) and sorting them, the filter returns the median value, which effectively reduces noise spikes. 
</p>
<ul>
  <li>Templated to allow a compile-time set of taps (<code>n</code>): helps ensure a small footprint and straightforward usage.</li>
  <li>Implements a well-known algorithm from N. Wirth’s book, with an implementation by N. Devillard.</li>
  <li>Useful for sensor data smoothing (e.g., encoders, ultrasonic, inertial).</li>
</ul>

<h3>2. PID Controller</h3>
<p>
  Within <code>src/lib/autoncontrol.cpp</code>, there is a function named <code>PIDController</code>. This function
  provides a proportional–integral–derivative control loop to maintain or reach specific targets (for example,
  course-correcting when following a route).
</p>
<ul>
  <li>The function calculates an <code>error</code> term, its <code>derivative</code>, and <code>integral</code> over
      time to produce an <code>output</code>.</li>
  <li>Implements output clamping (a maximum/minimum output), which helps prevent overshooting and integral wind-up.</li>
  <li>Useful for controlling drive train movement, motor speed, or other feedback systems where accuracy is important.</li>
</ul>

<h3>3. Graphical Library (LittlevGL)</h3>
<p>
  For creating graphical interfaces in embedded systems, the project includes references to <em>LittlevGL</em> (in
  <code>include/display/README.md</code>). The library allows for:
</p>
<ul>
  <li>Developing UI capabilities with minimal memory overhead.</li>
  <li>Supporting animation, touchscreen input, various widgets, and theming.</li>
  <li>A PC simulator for quick prototyping.</li>
</ul>
<p>
  While it is not heavily featured in the code snippets shown, it can be useful if you plan on extending your UI or debugging
  reactivity on embedded screens.
</p>

<h3>4. Autonomous Routing and Movement</h3>
<p>
  The code in <code>src/main.cpp</code> and <code>src/lib/autoncontrol.cpp</code> showcase a framework for autonomous route
  selection and <em>moveSteering</em> style commands. The steering approach is modular, making it easier to integrate
  additional sensor feedback loops (e.g., inertial sensor readings).
</p>
<ul>
  <li><code>moveSteering</code> calculates appropriate left-right power outputs to achieve a user-specified steering
      level, often combined with PID for fine control.</li>
  <li>Built to be easily adapted to various game or route strategies, storing references in global variables or enumerators
      for different routes (e.g., <code>RED_1</code>, <code>BLUE_1</code> in <code>autonomous()</code>).</li>
</ul>

<h2>How to Use</h2>
<ol>
  <li><strong>Clone or download</strong> this repository to your local machine.</li>
  <li><strong>Include and link</strong> the relevant headers (e.g., <code>medianFilter.hpp</code>) or
      library resources in your project.</li>
  <li><strong>Implement the filter or PID code</strong> in your robot's or embedded system's control loop for sensor
      data smoothing and stable control outputs.</li>
  <li>Modify or expand the <strong>autonomous route selection</strong> as needed in <code>autonomous()</code> (in
      <code>src/main.cpp</code>).</li>
</ol>
