---
layout: post
category: Python
tags: PyGame
title: Makeing Game with Python & Pygame（3）
---
	import pygame, sys
	from pygame.locals import *
	
	pygame.init()
	
	# set up the window
	DISPLAYSURF = pygame.display.set_mode((400, 300), 0, 32)
	pygame.display.set_caption('Drawing')
	
	# set up the colors
	BLACK = (  0,   0,   0)
	WHITE = (255, 255, 255)
	RED   = (255,   0,   0)
	GREEN = (  0, 255,   0)
	BLUE  = (  0,   0, 255)
	
	# draw on the surface object
	DISPLAYSURF.fill(WHITE)
	pygame.draw.polygon(DISPLAYSURF, GREEN, ((146, 0), (291, 106), (236, 277), (56, 277), (0, 106)))
	pygame.draw.line(DISPLAYSURF, BLUE, (60, 60), (120, 60), 4)
	pygame.draw.line(DISPLAYSURF, BLUE, (120, 60), (60, 120))
	pygame.draw.line(DISPLAYSURF, BLUE, (60, 120), (120, 120), 4)
	pygame.draw.circle(DISPLAYSURF, BLUE, (300, 50), 20, 0)
	pygame.draw.ellipse(DISPLAYSURF, RED, (300, 200, 40, 80), 1)
	pygame.draw.rect(DISPLAYSURF, RED, (200, 150, 100, 50))
	
	pixObj = pygame.PixelArray(DISPLAYSURF)
	pixObj[380][280] = BLACK
	pixObj[382][282] = BLACK
	pixObj[384][284] = BLACK
	pixObj[386][286] = BLACK
	pixObj[388][288] = BLACK
	del pixObj
	
	# run the game loop
	while True:
	    for event in pygame.event.get():
	        if event.type == QUIT:
	            pygame.quit()
	            sys.exit()
	    pygame.display.update()



![](http://bcs.duapp.com/blog-pyiner/qqq.jpg?sign=MBO:528b10b38a1b368b5a572d8d459f541b:5ETceXfzaAdGmtl6eRpTxjEyASM%3D)

**fill()**是pygame.Surface对象的一个方法 参数为一个颜色 填充整个pygame.Surface对象

**pygame.draw.polygon(surface, color, pointlist, width)**多边形绘制函数 前两个参数很容易理解 第三个参数为包含着一系列点坐标的元组或列表 第四个参数为线的宽度 第四个参数可以缺省 如果缺省的话整个多边形内部会被填满颜色

**pygame.draw.line(surface, color, start_point, end_point, width)**绘制直线

**pygame.draw.lines(surface, color, closed, pointlist, width)**绘制许多的直线 从第一个点开始一次连接相邻的两个点closed为布尔型变量 如果closed==True那么第一个点和最后一个点之间会有连线 如果
closed==False那么第一个点和最后一个点之间没有连线

**pygame.draw.circle(surface, color, center_point, radius, width)**绘制圆

**pygame.draw.ellipse(surface, color, bounding_rectangle, width)**绘制椭圆 需要特别解释的是bounding_rectangle参数 这个参数一个rect对象 表示椭圆外框矩形

# Pygame像素对象 #
当你需要对单个像素操作的话就需要Pygame像素对象了 pygame.PixelArray()函数可以创建一个pygame.PixelArray对象 参数为一个Surface对象

	pixObj = pygame.PixelArray(DISPLAYSURF)
当创建完成以后 这个Surface对象会被锁定 锁定以后绘图函数依然可以作用于Surface对象 但是无法使用blit()函数将图片绘制到Surface对象上
Surface对象的get_locked()属性为True的时候说明已经被锁定 为False的时候说明没有被锁定
像素对象可以用如下方式设置像素点颜色

	pixObj[480][380] = BLACK
当使用完像素对象以后使用del语句删除像素对象 同时对应的Surface对象会被解锁
	
	del pixObj
	pygame.display.update()函数
	pygame.display.update()函数只会将display Surface对象绘制到屏幕上 对于其他的Surface对象或图片 需要使用blit()函数将其绘制到display Surface对象上