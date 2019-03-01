# Yuliya Miatlionak

## Contacts:
  - email: metlenok.yulia@gmail.com
  - telegram: Yuliya_Metlenok

## Summary
I chose front-end development because I see the results of my work and there is a lot of information about it. I want to be a good specialist and nothing else. 
I use to work hard and learn at the same time because I agree with the quote from Alice in Wonderland by Lewis Carroll: 
> We must run as fast as we can, just to stay in place. And if you wish to go anywhere you must run twice as fast as that.


## Skills
- HTML5
- CSS3
- Java Script (including ES6 - ES8 features)
- React 16
- Bootstrap 4
- SCSS
- Webpack 4
- Git (GitHub)

## Education
I finished The Rolling Scopes School 2018-Q3.
My educational projects:  
* [rss-mentor-dashboard](https://juliamv.github.io/rss-mentor-dashboard/)
* [game](https://juliamv.github.io/game/)
* [youtube-client](https://juliamv.github.io/youtube-client/)
* [markup](https://juliamv.github.io/markup/)

## English level
A2

## Code examples
Table component from rss-mentor-dashboard

        import React from 'react';
        import propTypes from 'prop-types';
        import classes from './Table.module.css';

        const TaskCell = ({ link, name }) => (
            <td>
                <a href={link} target="_blank" rel="noopener noreferrer">{name}</a>
            </td>
        );

        TaskCell.propTypes = {
            name: propTypes.string.isRequired,
            link: propTypes.string,
        };

        TaskCell.defaultProps = {
            link: '',
        };

        const StudentNameCell = ({ name }) => (
            <th>
                <a
                    href={`https://github.com/rolling-scopes-school/${name}-2018Q3`}
                    target="_blank"
                    rel="noopener noreferrer"
                >
                    {name}
                </a>
            </th>
        );

        StudentNameCell.propTypes = {
            name: propTypes.string.isRequired,
        };

        const Table = ({ tasks, students }) => {
            const tableHeaderCells = [];
            tableHeaderCells[0] = <th key="row0cell0">Tasks</th>;
            students.forEach((student, index) => {
                tableHeaderCells.push(<StudentNameCell
                    name={student.studentGitHub}
                    checked={student.checkedTasks}
                    key={`row0cell${index + 1}`}
                />);
            });
            const tableBody = [];
            for (let i = 0; i < tasks.length; i += 1) {
                const tableBodyRow = [];
                tableBodyRow.push(<TaskCell
                    name={tasks[i].task}
                    link={tasks[i].link}
                    key={`row${i + 1}cell0`}
                />);
                for (let j = 1; j <= students.length; j += 1) {
                    const studentChekedTasks = students[j - 1].checkedTasks;
                    const currentStatus = studentChekedTasks.find(elem => elem === tasks[i].task);
                    let cell = <td key={`row${i + 1}cell${j}`} />;
                    if (currentStatus) {
                        cell = <td className={classes.checked} key={`row${i + 1}cell${j}`} />;
                    }
                    if (tasks[i].status === 'Checked' && !currentStatus) {
                        cell = <td className={classes.warning} key={`row${i + 1}cell${j}`} />;
                    }
                    tableBodyRow.push(cell);
                }
                tableBody.push(<tr data-status={tasks[i].status} key={`row${i}`}>{tableBodyRow}</tr>);
            }
            return (
                <table key="table" className={classes.Table}>
                    <thead key="thead">
                        <tr key="row0">
                            {tableHeaderCells}
                        </tr>
                    </thead>
                    <tbody key="tbody">
                        {tableBody}
                    </tbody>
                </table>
            );
        };

        Table.propTypes = {
            tasks: propTypes.arrayOf(propTypes.shape({
                task: propTypes.string,
                link: propTypes.string,
                status: propTypes.string,
            })).isRequired,
            students: propTypes.arrayOf(propTypes.shape({
                mentor: propTypes.string,
                studentGitHub: propTypes.string,
                interviewer: propTypes.string,
                checkedTasks: propTypes.array,
            })).isRequired,
        };

        export default Table;
