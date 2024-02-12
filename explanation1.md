Code 1: Delayed State Update
Explanation:
In React, the setState function (or setCount in this case) provided by the useState hook is asynchronous. This means that when you call setCount(count + 1), React schedules an update to the component's state but does not immediately apply it. Therefore, when you log the count immediately after calling setCount, you will see the older value because the state update has not yet been applied.

Solution:
To log the updated count value, you can use the useEffect hook with count as a dependency. This will ensure that the log statement runs after the state has been updated.







import React, { useState, useEffect } from 'react';

function App() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log(count); // Log the updated count value
  }, [count]);

  const handleClick = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <p>Button is clicked {count} times</p>
      <button onClick={handleClick}>Click Me</button>
    </div>
  );
}

export default App;







Code 2: Multiple State Updates
Explanation:
In React, state updates are batched together for performance reasons. When you call setCount multiple times in succession like setCount(count + 1) three times, React does not immediately update the state three times. Instead, it combines these updates into a single update, which means each subsequent call to setCount uses the same initial count value.

Solution:
To achieve the expected behavior of incrementing the count by 3, you can use the functional form of setCount, which takes the previous state as an argument. This ensures that each call to setCount uses the updated count value from the previous state.






import React, { useState } from 'react';

function App() {
  const [count, setCount] = useState(0);

  const handleClick = () => {
    setCount(prevCount => prevCount + 1);
    setCount(prevCount => prevCount + 1);
    setCount(prevCount => prevCount + 1);
  };

  return (
    <div>
      <p>Button is clicked {count} times</p>
      <button onClick={handleClick}>Click Me</button>
    </div>
  );
}


export default App;





Using the functional form of setCount, each call to setCount now updates the count based on the previous state, resulting in the count being incremented by 3 as expected.