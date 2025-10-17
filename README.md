jsx
import React, { useState } from 'react';

function App() {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [emailError, setEmailError] = useState(null);

  const validateEmail = (email) => {
    const emailRegex = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
    if (!emailRegex.test(email)) {
      setEmailError('Invalid email address');
    } else {
      setEmailError(null);
    }
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log('Form submitted:', { email, password });
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>Email:</label>
      <input
        type="email"
        value={email}
        onChange={(e) => {
          setEmail(e.target.value);
          validateEmail(e.target.value);
        }}
      />
      {emailError && <div style={{ color: 'red' }}>{emailError}</div>}
      <br />
      <label>Password:</label>
      <input
        type="password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
      />
      <br />
      <button
        type="submit"
        disabled={!email || password.length < 8 || emailError}
      >
        Submit
      </button>
    </form>
  );
}
