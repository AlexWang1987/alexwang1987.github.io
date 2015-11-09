# DOM

At early stage of front-end development, we sometimes have to manipulate DOM to implement our effects or change its structure based on our data dynamically. But as evolving of FE, we nearly don't need to operate them using "React-way".

###React-Way
React-way is an abstract way to update DOM, not manipulate directly, but base on the diffs. There is a virtual tree in memory which is faced to programmer. React-Engine's duty is to update its `diffs`. As a programmer, we don't event care how the virtual tree to be rendered. So, all DOM related operation has been separated from programmers.