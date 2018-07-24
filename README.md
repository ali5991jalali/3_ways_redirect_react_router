# 3_ways_redirect_react_router

I found 3 different ways for Redirect in recat-router...they are same in meaning but different in code view

way 1:

  <Route path="/protected" render={()=>(<Protected is_user={fakeAuth.is_user}/>)}>
  
  Protected Component:
  
  import React from 'react';

import {Redirect,withRouter} from 'react-router-dom';

class Protected extends React.Component{

render(){

if(this.props.isuser===true){

return (<div className="row" style={{textAlign:'center',marginTop:'120px',paddingLeft:'50%'}}>

<h1>Protected</h1>


</div>)

}else{

return <Redirect to={{pathname: "/login", state: { from: this.props.location }}}/>

}

}

} 

export default withRouter(Protected);





way 2:

<Route path="/protected" render={()=>(
  fakeAuth.is_user===true?
  <Protected/>:<Redirect to="/login">
  
  )}>
  
  Protected component:
  import React from 'react';

class Protected extends React.Component{

render(){

return (<div className="row" style={{textAlign:'center',marginTop:'120px',paddingLeft:'50%'}}>

<h1>Protected</h1>


</div>)

}

} 

export default Protected;

way 3:

<PrivateRoute path="/protected" component={Protected}/>


PrivateRoute Component:

const PrivateRoute=({component:Component,...rest})=>(

<Route {...rest} render={(props)=>(
fakeAuth.is_user===true?
<Component {...props}>:<Redirect to={{pathname:'/login',state:{from:props.location}}}/>

)}>

)

Protected Component:

import React from 'react';

class Protected extends React.Component{

render(){

return (<div className="row" style={{textAlign:'center',marginTop:'120px',paddingLeft:'50%'}}>

<h1>Protected</h1>


</div>)

}

} 

export default Protected;
