# assign-4
# Classes: Dealing with Complex Numbers
import math
class Complex:
    def __init__(self, a, b):
        self.a, self.b = a, b;
    def display(self):
        if self.a < 0.005 and self.a > -0.005:
            self.a = 0;
        if self.b < 0.005 and self.b > -0.005:
            self.b = 0;
        if self.a != 0:
            str1 = '%0.2f' % self.a;
            if self.b > 0:
                str1 += ' + %0.2fi' % self.b;
            elif self.b < 0:
                str1 += ' - %0.2fi' % -self.b;
        elif self.b != 0:
            str1 = '%0.2fi' % self.b;
        else:
            str1 = '0.00';
        print str1;
        
    def conjugate(self):
        return Complex(self.a, -self.b);
    def norm(self):
        return self.a*self.a + self.b*self.b;
    def scale(self, scalar):
        return Complex(self.a*scalar, self.b*scalar);

    
def add(a, b):
    return Complex(a.a + b.a, a.b + b.b);
def sub(a, b):
    return Complex(a.a - b.a, a.b - b.b);
def mul(a, b):
    return Complex(a.a * b.a - a.b * b.b, a.a * b.b + a.b * b.a);
def div(a, b):
    return mul(a, b.conjugate().scale(1.0/b.norm()));
    
x = Complex(0, 0);
y = Complex(0, 0);

[a, b] = raw_input().split();
x.a = float(a);
x.b = float(b);

[a, b] = raw_input().split();
y.a = float(a);
y.b = float(b);

add(x, y).display();
sub(x, y).display();
mul(x, y).display();
div(x, y).display();
print '%0.2f' % math.sqrt(x.norm());
print '%0.2f' % math.sqrt(y.norm());

# 
import math

class Points(object):

# Torsional Angle - START
    def __init__(self, x, y, z):
        self.x = x
        self.y = y
        self.z = z

    def __sub__(self, no):
        x = self.x - no.x
        y = self.y - no.y
        z = self.z - no.z
        return Points(x, y, z)

    def dot(self, no):
        x = self.x * no.x
        y = self.y * no.y
        z = self.z * no.z
        return x + y + z

    def cross(self, no):
        x = self.y * no.z - self.z * no.y
        y = self.z * no.x - self.x * no.z
        z = self.x * no.y - self.y * no.x
        return Points(x, y, z)

# Torsional Angle  -  END
    
    def absolute(self):
        return pow((self.x ** 2 + self.y ** 2 + self.z ** 2), 0.5)

if __name__ == '__main__':
    points = list()
    for i in range(4):
        a = list(map(float, input().split()))
        points.append(a)

    a, b, c, d = Points(*points[0]), Points(*points[1]), Points(*points[2]), Points(*points[3])
    x = (b - a).cross(c - b)
    y = (c - b).cross(d - c)
    angle = math.acos(x.dot(y) / (x.absolute() * y.absolute()))

    print("%.2f" % math.degrees(angle))
