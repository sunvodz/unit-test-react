# Unit Test React

![Screenshot from 2019-12-18 16-46-44](https://user-images.githubusercontent.com/42707869/71075907-6ececd80-21b7-11ea-8b84-7056148b87e3.png)
`
npx create-react-app unit-test-react
cd unit-test-react/
yarn add --dev enzyme enzyme-adapter-react-16
code .
`
edit file setupTest.js
`
import '@testing-library/jest-dom/extend-expect';
import Enzyme from 'enzyme';
import Adapter from 'enzyme-adapter-react-16'

Enzyme.configure({ adapter: new Adapter() })

add file Counter.js

import React, { Component } from 'react'
import "./Counter.css";

class Counter extends Component {
  state = { counter: 0 }

  render() {
    return (
      <div>
        <button id='test-add' onClick={() => {
          this.setState(prev => ({ counter: prev.counter + 1 }))
        }}>
          +
        </button>
          {this.state.counter} 
        <button id='test-sub' onClick={() => {
          this.setState(prev => ({ counter: prev.counter - 1 }))
        }}>
          -
        </button>
      </div>
    );
  }
}

export default Counter
`


add file Counter.test.js

`
import React from "react";
import { shallow } from "enzyme";

import Counter from "./Counter";

it("renders correctly", () => {
  const wrapper = shallow(<Counter />);
  expect(wrapper.find("#test-add")).toHaveLength(1);
  expect(wrapper.find("#test-sub")).toHaveLength(1);
  expect(wrapper.state("counter")).toBe(0);
});


`
RUN: yarn start


Edit file App.js
`
import React from "react";
import logo from "./logo.svg";
import "./App.css";
import Counter from "./Counter";
function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        TEST
        <Counter />
      </header>
    </div>
  );
}

export default App;

`
RUN TEST : yarn test


