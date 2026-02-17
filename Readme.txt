1-)[Budget Tracking ]
import { useState } from "react";

function BudgetTracker() {
  const [amount, setAmount] = useState("");
  const [list, setList] = useState([]);

  // Add Amount
  const addAmount = () => {
    if (amount.trim() === "") return;

    setList([...list, Number(amount)]);
    setAmount("");
  };

  // Delete Amount
  const deleteAmount = (index) => {
    const newList = list.filter((_, i) => i !== index);
    setList(newList);
  };

  // Calculate Total
  let total = 0;
  list.forEach((item) => {
    total += item;
  });

  return (
    <div>
      <h2>Simple Budget Tracker</h2>

      <h3>Balance: ₹ {total}</h3>

      <input
        type="number"
        placeholder="Enter amount (+/-)"
        value={amount}
        onChange={(e) => setAmount(e.target.value)}
      />

      <button onClick={addAmount}>Add</button>

      <ul>
        {list.map((item, index) => (
          <li key={index}>
            ₹ {item}
            <button onClick={() => deleteAmount(index)}>
              Delete
            </button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default BudgetTracker;

2-)[TO-DO]
import { useState } from "react";
import "./index.css"

function Todo(){
    const[task,setTask]=useState("");
    const[list,setList]=useState([]);

    const addTask=()=>{
        if(task.trim()==="")return;

        setList([...list,task]);
        setTask("");
    };

    const deleteTask=(index)=>{
        const newList=list.filter((_,i)=>i!==index);
        setList(newList);
    };

    return(
        <div>
            <h2>Todo App</h2>

            <input type="text" name="task" value={task} placeholder="Enter task" onChange={(e)=>setTask(e.target.value)}/><br/>

            <button onClick={addTask}>Add</button>
            <ul>
                {list.map((item,index)=>(
                    <li key={index}>
                        {item}
                        <button onClick={()=>deleteTask(index)}>Delete</button>
                    </li>
                ))}
            </ul>
        </div>
    );

}
export default Todo;


3-)Shopping -)
import { useState } from "react";

function ShoppingList() {
  const [item, setItem] = useState("");
  const [qty, setQty] = useState("");
  const [list, setList] = useState([]);

  // Add Item
  const addItem = () => {
    if (item.trim() === "" || qty === "") return;

    const newItem = {
      name: item,
      quantity: qty
    };

    setList([...list, newItem]);
    setItem("");
    setQty("");
  };

  // Delete Item
  const deleteItem = (index) => {
    const newList = list.filter((_, i) => i !== index);
    setList(newList);
  };

  return (
    <div>
      <h2>Shopping List</h2>

      <input
        type="text"
        placeholder="Item name"
        value={item}
        onChange={(e) => setItem(e.target.value)}
      />

      <input
        type="number"
        placeholder="Quantity"
        value={qty}
        onChange={(e) => setQty(e.target.value)}
      />

      <button onClick={addItem}>Add</button>

      <ul>
        {list.map((obj, index) => (
          <li key={index}>
            {obj.name} - {obj.quantity}
            <button onClick={() => deleteItem(index)}>
              Delete
            </button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default ShoppingList;


3-[Combined Form]
import { useState } from "react";

function CombinedForm(){

    const [name, setName] = useState("");
    const [email, setEmail] = useState("");
    const [password, setPassword] = useState("");
    const [message, setMessage] = useState("");
    const [topic, setTopic] = useState("General Inquiry");
    const [agree, setAgree] = useState(false);

    const [error, setError] = useState("");
    const [submittedData, setSubmittedData] = useState(null);
    const [success, setSuccess] = useState(false);

    const handleSubmit = (e) => {
        e.preventDefault();

        if(name === ""){
            setError("Name should not be empty!");
            return;
        }

        if(!email.includes("@")){
            setError("Enter valid email!");
            return;
        }

        if(password.length < 8){
            setError("Password must be at least 8 characters!");
            return;
        }

        if(message === ""){
            setError("Message cannot be empty!");
            return;
        }

        if(!agree){
            setError("You must agree to terms and conditions!");
            return;
        }

        setError("");
        setSuccess(true);

        setSubmittedData({
            name,
            email,
            password,
            message,
            topic
        });

        // Optional: Reset form after submit
        setName("");
        setEmail("");
        setPassword("");
        setMessage("");
        setTopic("General Inquiry");
        setAgree(false);
    };

    return(
        <div className="form-container">
            <h2>Complete Registration Form</h2>

            <form onSubmit={handleSubmit}>

                <label>Name</label>
                <input 
                    type="text"
                    value={name}
                    onChange={(e) => setName(e.target.value)}
                />

                <label>Email</label>
                <input 
                    type="text"
                    value={email}
                    onChange={(e) => setEmail(e.target.value)}
                />

                <label>Password</label>
                <input 
                    type="password"
                    value={password}
                    onChange={(e) => setPassword(e.target.value)}
                />

                <label>Message</label>
                <textarea
                    value={message}
                    onChange={(e) => setMessage(e.target.value)}
                ></textarea>

                <label>Topic</label>
                <select
                    value={topic}
                    onChange={(e) => setTopic(e.target.value)}
                >
                    <option>General Inquiry</option>
                    <option>Feedback</option>
                    <option>Support</option>
                    <option>Complaint</option>
                </select>

                <br/><br/>

                <input
                    type="checkbox"
                    checked={agree}
                    onChange={(e) => setAgree(e.target.checked)}
                />
                <label>I agree to terms and conditions</label>

                <br/><br/>

                <button type="submit">Submit</button>

            </form>

            {/* Error Message */}
            {error && <p style={{color:"red"}}>{error}</p>}

            {/* Success Message */}
            {success && <p style={{color:"green"}}>Form submitted successfully!</p>}

            {/* Submitted Data */}
            {submittedData && (
                <div className="result">
                    <h3>Submitted Details</h3>
                    <p><b>Name:</b> {submittedData.name}</p>
                    <p><b>Email:</b> {submittedData.email}</p>
                    <p><b>Password:</b> {submittedData.password}</p>
                    <p><b>Message:</b> {submittedData.message}</p>
                    <p><b>Topic:</b> {submittedData.topic}</p>
                </div>
            )}

        </div>
    );
}

export default CombinedForm; 


4-)[Book]

import React from 'react';

const Book = ({ title, author, image }) => {
  return (
    <div>
      <img src={image} alt={title} width="150" />
      <h3>{title}</h3>
      <p>{author}</p>
    </div>
  );
};

export default Book;

import React, { Component } from 'react';
import Book from './Book';
import img1 from '../assets/img1.jpg';
import img2 from '../assets/img2.jpg';
import img3 from '../assets/img3.jpg';

class BookStore extends Component {
  render() {
    return (
      <div>
        <h1>Book Store</h1>

        <Book
          title="The Great Gatsby"
          author="F. Scott Fitzgerald"
          image={img1}
        />

        <Book
          title="1984"
          author="George Orwell"
          image={img2}
        />

        <Book
          title="JoelBook3"
          author="Joel Gonsalves"
          image={img3}
        />
      </div>
    );
  }
}

export default BookStore;
