function [sol_x, sol_y, sol_z] = task_1

	t = 0 : 0.05 : 5;
	h = [0.6, 0.03, 0.02];
    
	[sol_x, sol_y, sol_z] = dsolve ('Dx = x + y + z + sin(t)', 'Dy = x + y - 2*z + sin(t)',  'Dz = x - y - z', 'x(0) = 1', 'y(0) = 1', 'z(0) = 1');

	plot(t, eval(sol_y), 'k');
	hold on
	axis([0, 1.5, 0, 15]) 
	grid on

	for k = 1 : length(h)
        
		t_range = 0 : h(k) : 5;
        
        x = ones(size(t_range)); 	
        y = ones(size(t_range)); 		
        z = ones(size(t_range)); 		

            for n = 1 : length(t_range) - 1
                x(n + 1) = x(n) + h(k) * (x(n) + y(n) + z(n) + sin(t_range(n)));
                y(n + 1) = y(n) + h(k) * (x(n) + y(n) - 2 * z(n) + sin(t_range(n)));
                z(n + 1) = z(n) + h(k) * (x(n) - y(n) - z(n));
            end
		
            if k == 1        
                plot(t_range, y, 'g');
            end

            if k == 2
                plot(t_range, y, 'r');
            end
            
            if k == 3
                plot(t_range, y, 'b');
            end
	end

	legend show
	legend({'y(t)', 'h_1 = 0.6', 'h_2 = 0.03', 'h_3 = 0.02'}, 'Location', 'northwest')
    xlabel('t')
    ylabel('y(t)')
    
end

% sol_x =     (13*exp(2*t))/15 
%           + 1/(6*exp(13^(1/2)*t)^(1/2)*exp(t)^(1/2)) 
%           + exp(13^(1/2)*t)^(1/2)/(6*exp(t)^(1/2)) 
%           - (5^(1/2)*cos(t - atan(2)))/5 
%           - (11*13^(1/2))/(78*exp(13^(1/2)*t)^(1/2)*exp(t)^(1/2)) 
%           + (11*13^(1/2)*exp(13^(1/2)*t)^(1/2))/(78*exp(t)^(1/2));

% sol_y =     (13*exp(2*t))/15 
%           + 1/(6*exp(13^(1/2)*t)^(1/2)*exp(t)^(1/2)) 
%           + exp(13^(1/2)*t)^(1/2)/(6*exp(t)^(1/2)) 
%           - (5^(1/2)*cos(t - atan(2)))/5 
%           + (7*13^(1/2))/(78*exp(13^(1/2)*t)^(1/2)*exp(t)^(1/2)) 
%           - (7*13^(1/2)*exp(13^(1/2)*t)^(1/2))/(78*exp(t)^(1/2));

% sol_z =     1/(2*exp(13^(1/2)*t)^(1/2)*exp(t)^(1/2)) 
%           + exp(13^(1/2)*t)^(1/2)/(2*exp(t)^(1/2)) 
%           + 13^(1/2)/(26*exp(13^(1/2)*t)^(1/2)*exp(t)^(1/2)) 
%           - (13^(1/2)*exp(13^(1/2)*t)^(1/2))/(26*exp(t)^(1/2));