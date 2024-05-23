# React - Add more form fields dynamically

```js
import React, { useState } from "react";

const userObj = {
  name: "",
  email: "",
  jobs: [{ company: "", exp: "1" }],
  skills: [{ name: "", rate: "1" }],
};

const App = () => {
  const [user, setUser] = useState(userObj);
  const [userList, setUserList] = useState([]);

  const onChangeCompanyNameHandler = (evt, index) => {
    let userJobs = [...user.jobs];
    userJobs[index].company = evt.target.value;
    setUser({ ...user, jobs: userJobs });
    //console.log(userJobs);
  };

  const onChangeExpHandler = (evt, index) => {
    let userJobs = [...user.jobs];
    userJobs[index].exp = evt.target.value;
    setUser({ ...user, jobs: userJobs });
    //console.log(userJobs);
  };

  const addMoreJobHandler = () => {
    setUser({ ...user, jobs: [...user.jobs, { company: "", exp: "1" }] });
  };

  const removeJobHandler = (index) => {
    let userJobs = [...user.jobs];
    userJobs.splice(index, 1);
    setUser({ ...user, jobs: userJobs });
  };

  const onChangeSkillNameHandler = (evt, index) => {
    let userSkills = [...user.skills];
    userSkills[index].name = evt.target.value;
    setUser({ ...user, skills: userSkills });
    //console.log(userSkills);
  };

  const onChangeSkillRateHandler = (evt, index) => {
    let userSkills = [...user.skills];
    userSkills[index].rate = evt.target.value;
    setUser({ ...user, skills: userSkills });
    //console.log(userSkills);
  };

  const addMoreSkillHandler = () => {
    setUser({ ...user, skills: [...user.skills, { name: "", rate: "1" }] });
  };

  const removeSkillHandler = (index) => {
    let userSkills = [...user.skills];
    userSkills.splice(index, 1);
    setUser({ ...user, skills: userSkills });
  };

  const formSubmitHandler = (e) => {
    e.preventDefault();
    setUserList([...userList, user]);
    resetForm();
    console.log(userList);
  }

  const formResetHandler = () => {
    resetForm();
  }

  const resetForm = () => {
    const resetUserObj = {
      name: "",
      email: "",
      jobs: [{ company: "", exp: "1" }],
      skills: [{ name: "", rate: "1" }],
    };
    setUser(resetUserObj);
  }

  return (
    <>
      <div className="container">
        <div className="row mt-2">
          <h1>React - Add more form fields dynamically</h1>
          <hr />
        </div>
        <div className="row mt-3">
          <div className="col-md-6">
            <form onSubmit={formSubmitHandler}>
              <div className="row">
                <div className="col-md-8">
                  <div className="form-group">
                    <label htmlFor="name">Name:</label>
                    <input
                      type="text"
                      name="name"
                      id="name"
                      className="form-control"
                      required
                      placeholder="Enter Name"
                      value={user.name}
                      onChange={(e) =>
                        setUser({ ...user, name: e.target.value })
                      }
                    />
                  </div>
                  <div className="form-group">
                    <label htmlFor="email">Email:</label>
                    <input
                      type="email"
                      name="email"
                      id="email"
                      className="form-control"
                      required
                      placeholder="Enter Email"
                      value={user.email}
                      onChange={(e) =>
                        setUser({ ...user, email: e.target.value })
                      }
                    />
                  </div>
                </div>
              </div>
              <div className="row mt-2">
                <div className="col-md-12">
                  <strong>Job (s)</strong>
                </div>
              </div>
              {user.jobs.length > 0 &&
                user.jobs.map((item, index) => {
                  return (
                    <div className="row mt-2" key={"jobs" + index}>
                      <div className="col-md-8">
                        <div className="form-group">
                          <input
                            type="text"
                            name={"company[" + index + "]"}
                            id={"company" + index}
                            className="form-control"
                            required
                            placeholder="Company"
                            value={item.company || ""}
                            onChange={(e) =>
                              onChangeCompanyNameHandler(e, index)
                            }
                          />
                        </div>
                      </div>
                      <div className="col-md-3">
                        <div className="form-group">
                          <input
                            type="number"
                            name={"exp[" + index + "]"}
                            id={"exp" + index}
                            className="form-control"
                            min="1"
                            max="30"
                            maxLength="2"
                            required
                            placeholder="Exp"
                            value={item.exp}
                            onChange={(e) => onChangeExpHandler(e, index)}
                          />
                        </div>
                      </div>
                      <div className="col-md-1">
                        <div className="form-group">
                          {index > 0 && (
                            <button
                              type="button"
                              id={"jobDeleteBtn" + index}
                              className="btn btn-sm btn-danger"
                              onClick={() => removeJobHandler(index)}
                            >
                              [-]
                            </button>
                          )}
                        </div>
                      </div>
                    </div>
                  );
                })}
              <div className="row mt-2">
                <div className="col-md-12">
                  <button
                    type="button"
                    className="btn btn-sm btn-primary"
                    onClick={addMoreJobHandler}
                  >
                    [+]
                  </button>
                </div>
              </div>
              <div className="row mt-2">
                <div className="col-md-12">
                  <strong>Skill (s)</strong>
                </div>
              </div>
              {user.skills.length > 0 &&
                user.skills.map((item, index) => {
                  return (
                    <div className="row mt-2" key={"skills" + index}>
                      <div className="col-md-8">
                        <input
                          type="text"
                          name={"skill_name[" + index + "]"}
                          id={"skillName" + index}
                          className="form-control"
                          placeholder="Skill"
                          required
                          value={item.name}
                          onChange={(e) => onChangeSkillNameHandler(e, index)}
                        />
                      </div>
                      <div className="col-md-3">
                        <select
                          name={"skill_rate[" + index + "]"}
                          id={"skillRate" + index}
                          className="form-select"
                          onChange={(e) => onChangeSkillRateHandler(e, index)}
                          value={item.rate}
                        >
                          <option value="1">1</option>
                          <option value="2">2</option>
                          <option value="3">3</option>
                          <option value="4">4</option>
                          <option value="5">5</option>
                        </select>
                      </div>
                      <div className="col-md-1">
                        {
                          index > 0 && (
                            <button
                              type="button"
                              id={"removeSkillBtn" + index}
                              className="btn btn-sm btn-danger"
                              onClick={() => removeSkillHandler(index)}
                            >
                              [-]
                            </button>
                          )
                        }
                      </div>
                    </div>
                  );
                })}
              <div className="row mt-2">
                <div className="col-md-12">
                  <button
                    type="button"
                    className="btn btn-sm btn-primary"
                    onClick={addMoreSkillHandler}
                  >
                    [+]
                  </button>
                </div>
              </div>
              <div className="row mt-3">
                <div className="col-md-12">
                  <button
                    type="submit"
                    className="btn btn-success"
                  >
                    SAVE ALL
                  </button>
                  <button
                    type="button"
                    className="btn btn-danger mx-2"
                    onClick={formResetHandler}
                  >
                    Cancel
                  </button>
                </div>
              </div>
            </form>
          </div>
          <div className="col-md-6">
            <div style={{textAlign: 'right', fontWeight: 600}}>Total Users: ({userList.length})</div>
            <table className="table table-sm table-bordered table-hover">
              <thead>
                <tr>
                  <th>SL</th>
                  <th>NAME</th>
                  <th>EMAIL</th>
                  <th>JOB</th>
                  <th>SKILL</th>
                </tr>
              </thead>
              <tbody>
                {
                  userList.length > 0 &&
                    userList.map((item, index) => {
                      return (
                        <tr key={"userListTr" + index}>
                          <td>{index + 1}</td>
                          <td>{item.name || ''}</td>
                          <td>{item.email || ''}</td>
                          <td>
                            {
                              item.jobs.length > 0 &&
                                item.jobs.map((job, jobIndex) => {
                                  return (
                                    <li key={"userJob" + index + jobIndex}>{job.company} <small><i>[{job.exp + "Yrs"}]</i></small></li>
                                  )
                                })
                            }
                          </td>
                          <td>
                            {
                              item.skills.length > 0 &&
                                item.skills.map((skill, skillIndex) => {
                                  return (
                                    <li key={"userSkill" + index + skillIndex}>{skill.name} <small><i>({skill.rate})</i></small></li>
                                  )
                                })
                            }
                          </td>
                        </tr>
                      )
                    })
                }
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </>
  );
};

export default App;

```