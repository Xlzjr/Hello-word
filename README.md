
package com.mvc.control;
 
import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
 
import com.mvc.bean.*;
 
import com.mvc.dao.*;
/**
 * Servlet implementation class Servlet
 */
@WebServlet("/LoginServlet")
public class LoginServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    /**
     * @see HttpServlet#HttpServlet()
     */
    public LoginServlet() {
        super();
        // TODO Auto-generated constructor stub
    }
	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		response.getWriter().append("Served at: ").append(request.getContextPath());
	}
 
	/**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		 	String userNameInput = request.getParameter("name");
	        String passwordInput = request.getParameter("pwd");
	        	
	        String type=request.getParameter("type");
	        System.out.println(type);
	        //判断类型
	        if("2".equals(type)){
	        
	        StaffBean loginBeanInput = new StaffBean(); // Bean classes are efficiently used to access user information wherever required in the application.
	        loginBeanInput.setName(userNameInput);
	        loginBeanInput.setPwd(passwordInput);
 
	        LoginStaffDao loginDao = new LoginStaffDao();
	        
	        String userValidate = loginDao.authenticateUser(loginBeanInput);

	       
	        if(userValidate.equals("SUCCESS")){
	            System.out.print("SUCCESSyes");
	            request.setAttribute("userNameInput", userNameInput); //with setAttribute() you can define a "key" and value pair so that you can get it in future using getAttribute("key")
	            request.getRequestDispatcher("/h_main.jsp").forward(request, response);//RequestDispatcher is used to send the control to the invoked page.
	        }
 
	        else{
	            System.out.print("SUCCESSno");
	            request.setAttribute("errMessage", userValidate); // Here the error message returned from function has been stored in a errMessage key.
	            request.getRequestDispatcher("/login.jsp").forward(request, response);//forwarding the request
	        }
	        }
	        
	        else
	        {
		        UserBean loginBeanInput = new UserBean(); // Bean classes are efficiently used to access user information wherever required in the application.
		        loginBeanInput.setName(userNameInput);
		        loginBeanInput.setPwd(passwordInput);
		        
		        
		        LoginUserDao loginDao = new LoginUserDao();
		        
		        int userValidate =  loginDao.authenticateUser(loginBeanInput);
		        
		        if(userValidate!=-1){
		            System.out.print("SUCCESSyes");
		            //request.setAttribute("UID", userValidate);
		            request.setAttribute("userNameInput", userNameInput); //with setAttribute() you can define a "key" and value pair so that you can get it in future using getAttribute("key")
		            request.getRequestDispatcher("KMGP.jsp?uid="+userValidate).forward(request, response);//RequestDispatcher is used to send the control to the invoked page.
		        }
 
		        else{
		            System.out.print("SUCCESSno");
		            request.setAttribute("errMessage", userValidate); // Here the error message returned from function has been stored in a errMessage key.
		            request.getRequestDispatcher("/login.jsp").forward(request, response);//forwarding the request
		        }
	        }
	}
 
}
