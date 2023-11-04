import dash.testing
import dash
import dash_daq
import dash_bootstrap_components as dbc
import dash_core_components as dcc
import dash_html_components as html
import pytest

from sales_visualizer import app

@pytest.fixture
def client():
    # Create a test client for your Dash app
    return app.server.test_client()

def test_header_present(client):
    # Check if the header is present in the layout
    response = client.get('/')
    assert dcc.Markdown("Pink Morsel Sales Visualizer") in response.data

def test_visualization_present(client):
    # Check if the visualization is present in the layout
    response = client.get('/')
    assert dcc.Graph('line-chart') in response.data

def test_region_picker_present(client):
    # Check if the region picker is present in the layout
    response = client.get('/')
    assert dcc.RadioItems('region-selector') in response.data
    assert dcc.RadioItems('region-selector').type == 'radio'

if __name__ == '__main__':
    pytest.main(['-sv', __file__])
